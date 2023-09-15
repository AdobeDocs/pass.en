---
title: Integrating the Media Token Verifier
description: Integrating the Media Token Verifier
exl-id: 1688889a-2e30-4d66-96ff-1ddf4b287f68
---
# Integrating the Media Token Verifier

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## About the Media Token Verifier {#about-media-token-verifier}

When authorization succeeds, Adobe Pass authentication creates a long-lived authorization (AuthZ) token.  The AuthZ token is either passed to the client-side or stored on the server-side, depending upon the client's platform.  (See [Understanding Tokens](/help/authentication/programmer-overview.md#understanding-tokens) for how tokens are stored on different client systems, along with other details.)
 

An AuthZ token authorizes the user of the site to view a given resource.  It has a typical time-to-live (TTL) of 6 to 24 hours, after which the token expires. **For actual viewing access, the Adobe Pass authentication uses the AuthZ token to generate a short-lived media token that you obtain and pass to your media server**. These short-lived media tokens have a very brief TTL (typically, a few minutes).
 

In AccessEnabler integrations, you obtain the short-lived media token via the `setToken()` callback. For Clientless API integrations, you obtain the short-lived Media token with the `<SP_FQDN>/api/v1/tokens/media` API call. The token is a string sent in clear text, signed by Adobe, using token protection based on PKI (Public Key Infrastructure). With this PKI-based protection, the token is signed using an asymmetric key, issued to Adobe by a certification authority.
 

Because there is no validation on the client side for the token, a malicious user could use tools to inject fake `setToken()` calls. Therefore you **cannot** rely simply on the fact that `setToken()` was triggered, when considering whether a user is authorized or not. You must validate that the short-lived token itself is legitimate. The tool to perform the validation is the Media Token Verifier Library.
 

>[!TIP]
>
>You must pass the entire length of the returned token string to the Media Token Verifier for validation.

## Validating Short-lived Tokens with the Media Token Verifier {#validate-short-livedttokens}

We recommend that Programmers send the token to a web service that uses the Media Token Verifier Library, in order to validate the token before actually starting the video stream. The very short TTL of the short-lived media tokens is defined to be sufficiently long to allow for clock-synchronization issues between the server generating the token and the server validating the token, but no longer.

 

The [Media Token Verifier Library](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&theme=hc&locale=en-us&brand_id=343429&auth_origin=343429%2Cfalse%2Ctrue){target=_blank} is available for Adobe Pass authentication partners.

 

The Media Token Verifier library is contained in the Java archive `mediatoken-verifier-VERSION.jar`. The library defines:

* A token-verification API (`ITokenVerifier` interface), with JavaDoc documentation
* The Adobe public key used to verify that the token does indeed come from Adobe
* A reference implementation (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) that shows how to use the Verifier API and how to use the Adobe public key contained in the library to verify its origin
 

The archive contains all dependencies and certificate keystores. The default password for the included certificate keystore is "123456".

* The verification library requires JDK version 1.5 or higher.
* Use your preferred JCE provider for the signature algorithm, "SHA256WithRSA".
 

**The Verifier Library must be the only means used to analyze the token content. Programmers should not parse the token and extract the data themselves, because the token format is not guaranteed and is subject to future change.** Only the Verifier API is guaranteed to function correctly. Parsing the string directly might work temporarily, but cause problems in the future when the format might change. The Verifier API retrieves information from the token, such as:

* Is the token valid (the `isValid()` method)?
* The resource ID tied to the token (the `getResourceID()` method); this can be compared to (and it should match) the other parameter of the `setToken()` function callback. If it doesn't match, this might indicate fraudulent behavior.
* The time the token was issued (`getTimeIssued()` method).
* The TTL (`getTimeToLive()` method).
* An anonymized authentication GUID received from the MVPD (`getUserSessionGUID()` method).
* The distributor's ID that authenticated the user and if it is the case - the proxy-MVPD that provided the authentication for the distributor.

## Using the Verifier API {#using-verifier-api}

The `ITokenVerifier` class defines methods you use to validate token authenticity for a given resource. Use the `ITokenVerifier` methods to analyze a token received in response to a `setToken()` request.
 

The `isValid()` method is the primary means of validating a token. It takes one argument, a resource ID. If you pass a null resource ID, the method validates only the token authenticity and validity period.
 

The `isValid()` method returns one of these status values:

 

|      VALID_TOKEN     |         All validations succeeded         |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | Token format is invalid                   |
| INVALID_SIGNATURE    | Token authenticity could not be validated |
| TOKEN_EXPIRED        | Token TTL is not valid                    |
| INVALID_RESOURCE_ID  | Token not valid for given resource        |
| ERROR_UNKNOWN        | Token has not been validated yet          |

Additional methods provide specific access to the resource ID, the time issued, and the time-to-live for a given token.

* Use `getResourceID()` to retrieve the resource ID associated with the token and compare it to the ID returned from the setToken() request.
* Use `getTimeIssued()` to retrieve the time the token was issued.
* Use `getTimeToLive()` to retrieve the TTL.
* Use `getUserSessionGUID()` to retrieve an anonymized GUID set by the MVPD.
* Use `getMvpdId()` to retrieve the ID of the MVPD which authenticated the user.
* Use `getProxyMvpdId()` to retrieve the ID of the Proxy MVPD which authenticated the user.

## Sample Code {#sample-code}

The Media Token Verifier archive contains a reference implementation (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) and an example of invoking the API with the test class. This sample (`com.adobe.entitlement.text.EntitlementVerifierTest.java`) illustrates the integration of the token verification library into a media server.

 
```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
