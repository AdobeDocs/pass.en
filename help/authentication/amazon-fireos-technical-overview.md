---
title: Amazon FireOS Technical Overview
description: Amazon FireOS Technical Overview
exl-id: 939683ee-0dd9-42ab-9fde-8686d2dc0cd0
---
# Amazon FireOS Technical Overview {#amazon-fireos-technical-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#intro}

Amazon FireOS AccessEnabler is represented by two components : an AccessEnabler stub library used by the application and a system level Java Android library that enables mobile apps to use Adobe Pass authentication for TV Everywhere's entitlement services. An Android implementation for Amazon FireOS consists of the AccessEnabler interface that defines the entitlement API, and an EntitlementDelegate protocol that describes the callbacks that the library triggers. The system level AccessEnabler Android library enables access to Amazon services to enable Single Sing On at platform level.

## Understanding Native Client Workflows {#native_client_workflows}

Native client workflows are typically the same as, or very similar to, those of browser-based Adobe Pass authentication clients. However, there are a few exceptions, as described below.


### Post-initialization Workflow {#post-init}

All of the entitlement workflows supported by the AccessEnabler assume that you have previously called [`setRequestor()`](#setRequestor) to establish your identity. You make this call to provide your Requestor ID only once, usually during your application's initialization/setup phase.

With the native clients (e.g., AmazonFireOS), after your initial call to [`setRequestor()`](#setRequestor), you have a choice as to how to proceed:

- You can start making entitlement calls immediately and allow them to be queued silently, if needed.
- Or, you can receive a confirmation of the success/failure of [`setRequestor()`](#setRequestor) by implementing the setRequestorComplete() callback.
- Or, do both.

It is up to you as to whether to wait for notification of the success of [`setRequestor()`](#setRequestor) or to rely on the AccessEnabler's call queue mechanism. Since all subsequent authorization and authentication requests need the requestor ID and the associated configuration information, the [`setRequestor()`](#setRequestor) method effectively blocks all authentication and authorization API calls until initialization is complete.

### Generic Initial Authentication Workflow {#generic}

The purpose of this workflow is to log in a user with their MVPD.  After a successful login, the backend server issues the user an authentication token. While authentication is typically done as part of the authorization process, the following describes how authentication can work in isolation, and does not include any authorization steps.  

Note that while the following native client workflow differs from the typical browser-based authentication workflow, steps 1-5 are the same for both native clients and browser-based clients:

1.  Your page or player initiates the authentication workflow with a call to [getAuthentication()](#getAuthN), which checks for a valid cached authentication token. This method has an optional `redirectURL` parameter; if you do not supply a value for `redirectURL`, after a successful authentication the user is returned to the URL from which the authentication was initialized.
1.  The AccessEnabler determines the current authentication status. If the user is currently authenticated, the AccessEnabler calls your `setAuthenticationStatus()` callback function, passing an authentication status indicating success (Step 7 below).
1.  If the user is not authenticated, the AccessEnabler continues the authentication flow by determining whether the user's last authentication attempt was successful with a given MVPD. If an MVPD ID is cached AND the `canAuthenticate` flag is true OR an MVPD was selected using [`setSelectedProvider()`](#setSelectedProvider), the user is not prompted with the MVPD selection dialog. The authentication flow continues using the cached value of the MVPD (that is, the same MVPD that was used during the last successful authentication). A network call is made to the backend server, and the user is redirected to the MVPD login page (Step 6 below).
1.  If no MVPD ID is cached AND no MVPD was selected using [`setSelectedProvider()`](#setSelectedProvider) OR the `canAuthenticate` flag is set to false, the [`displayProviderDialog()`](#displayProviderDialog) callback is called. This callback directs your page or player to create the UI that presents the user with a list of MVPDs to choose from. An array of MVPD objects is provided, containing the necessary information for you to build the MVPD selector. Each MVPD object describes an MVPD entity and contains information such as the ID of the MVPD (e.g., XFINITY, AT\&T, etc.) and the URL where the MVPD logo can be found.
1.  Once a particular MVPD is selected, your page or player must inform the AccessEnabler of the user's choice. For non-Flash clients, once the user selects the desired MVPD, you inform the AccessEnabler of the user selection via a call to the [`setSelectedProvider()`](#setSelectedProvider) method. Flash clients instead dispatch a shared `MVPDEvent` of type "`mvpdSelection`", passing the selected provider.
1.  For Amazon applications, the [`navigateToUrl()`](#navigagteToUrl) callback will be ignored. The Access Enabler library facilitate access to a common WebView control to authenticate users.
1.  Via the `WebView`, the user arrives on the MVPD's login page and inputs their credentials. Note that several redirect operations occur during this transfer. 
1.  Once the WebView will finalize the authenticaiton, it will close and informs the AccessEnabler that the user has logged in successfully, the AccessEnabler retrieves the actual authentication token from the backend server. The AccessEnabler calls the [`setAuthenticationStatus()`](#setAuthNStatus) callback with a status code of 1, indicating success. If there is an error during the execution of these steps, the [`setAuthenticationStatus()`](#setAuthNStatus) callback is triggered with a status code of 0, along with a corresponding error code, indicating that the user is not authenticated.

### Logout Workflow {#logout}

For native clients, logouts are handled similarly to the authentication process described above. Following this pattern, the AccessEnabler will create a `WebView` control and will load the control with the URL of the logout endpoint on the backend server. Once the logout process is complete, the tokens are cleared.  

Note that the logout flow differs from the authentication flow in that the user is not required to interact with the `WebView` in any way. Once logout is complete, the AccessEnabler calls the `setAuthenticationStatus()` callback with a status code of 0, indicating that the user is not authenticated.

## Tokens {#tokens}

### Definitions and Usage {#definitions}

The Adobe Pass authentication entitlement solution revolves around the generation of specific pieces of data (tokens) that Adobe Pass authentication generates upon the successful completion of the authentication and authorization workflows. These tokens are stored locally on the client's Amazon FireOS device.

Tokens have a limited lifespan; upon expiration, tokens need to be re-issued through the re-initiation of the authentication and/or authorization workflows.

There are three types of tokens issued during the entitlement workflows:

- **Authentication token** - The end result of the user authentication workflow will be an authentication GUID that the AccessEnabler can use to make authorization queries on the user's behalf. This authentication GUID will have an associated time-to-live (TTL) value which may be different from the user's authentication session itself. Adobe Pass authentication generates an authentication token by binding the authentication GUID to the device initiating the authentication requests.
- **Authorization token** - Grants access to a specific protected resource identified by a unique `resourceID`. It consists of an authorization grant issued by the authorizing party along with the original `resourceID`. This information is bound to the device initiating the request.
- **Short-lived media token** - The AccessEnabler grants access to the hosting application for a given resource by returning a short-lived Media Token. This token is generated based on the authorization token that was previously acquired for that specific particular resource. Also, this token is not bound to the device, and the associated life-span is significantly shorter (default: 5 minutes).

Upon successful authentication and authorization, Adobe Pass authentication will issue authentication, authorization and short-lived media tokens. These tokens should be cached on the user's device and used for the duration of their associated life-spans.

### Caching Guidelines {#caching}


#### Authentication Token

- **AccessEnabler 1.10.1 for FireOS** is based on AccessEnabler for Android 1.9.1 - This SDK introduces a new method of token storage, enabling multiple Programmer-MVPD buckets, and therefore, multiple authentication tokens. 

#### Authorization Token

At any given moment only ONE authorization token per resource gets cached by the AccessEnabler. There can be multiple authorization tokens cached, but they are associated with different resources. Whenever a new authorization token is issued and an old one already exists for the same resource, the new token overwrites the existing cached value.

#### Media Token 

The short-lived media token should NOT be cached at all. The media token should be retrieved from the server every time an authorization API is called, because it is restricted to one-time use.

### Persistence {#persistence}

Tokens need to be persistent across consecutive runs of the same application. This means that once the authentication and authorization tokens have been acquired and the user closes the application, the same tokens are available to the application when the user re-opens the application. Moreover, it is desirable that these tokens be persistent across multiple applications. In other words, after a user uses one application to login with a specific identity provider (successfully obtaining authentication and authorization tokens), the same tokens can be used through a different application, and the user is no longer prompted for credentials when logging in via the same identity provider.

This type of seamless authentication / authorization workflow is what makes the Adobe Pass authentication solution a true TV-Everywhere implementation. From a pure engineering point of view, the Android AccessEnabler library works around the issues of cross-application data sharing by storing the token data into a database file located on external storage. This system-level shared resources provides the key ingredients that enable the implementation of the desired persistent tokens use-case:

- Support for structured storage - The Adobe Pass authentication token storage is not just a simple linear buffer-like memory structure. It provides a dictionary-like storage mechanism that allows for data indexing based on user-specified key values.
- Support for data persistence using the underlying file system - The contents of the database file are persisted by default and the data is saved on the device's external memory.

Once a particular token is placed into the token cache, its validity will be checked at different times by the AccessEnabler library.  A valid token is defined as:

- The token's TTL has not expired
- The issuer of the token is included in the list of allowed identity providers

The token storage can support multiple Programmer-MVPD combinations, relying on a multi-level nested map structure that can hold multiple authentication tokens. This new storage does not affect the AccessEnabler public API in any way and does not require changes on the Programmer's side. Here is an example that illustrates this newer functionality:

1.  Open App1 (developed by Programmer1).
1.  Authenticate with MVPD1 (which is integrated with Programmer1).
1.  Suspend / Close the current application, and open App2 (developed by Programmer2).
1.  Let's assume that Programmer2 is not integrated with MVPD2; therefore, the user will NOT be authenticated in App2.
1.  Authenticate with MVPD2 (which is integrated with Programmer2) in App2.
1.  Switch back to App1; the user will still be authenticated with Programmer1.

### Format {#format}

#### Authentication Token {#authn_token}

The listing below presents the format of the authentication token:

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthenticationToken>
        <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
        <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>   
    </simpleAuthenticationToken>
```
 

#### Authorization Token {#authz_token}

The listing below presents the format of the authorization token:

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthorizationToken>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
        <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>
    </simpleAuthorizationToken>
```


#### Short Media Token {#short_media_token}

The listing below presents the format of the short media token.  This token is exposed to the Programmer's application.  It is passed to the Programmer's application at the end of a successful entitlement process:

```JSON
    <signatureInfo>signature<signatureInfo>
    <shortAuthorizationToken>
      <sessionGUID>session_guid</sessionGUID>
      <requestorID>requestor_id</requestorID>
      <resourceID>resource_id</resourceID>
      <ttl>ttl_in_ms</ttl>
      <issueTime>issue_time</issueTime>
      <mvpdId>mvpd_id</mvpdId>
      <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
    </shortAuthorizationToken>
```
 

#### Device Binding {#device_binding}

In the XML listings above, note the tag entitled `simpleTokenFingerprint`. The purpose of this tag is to hold native device ID individualization info. The AccessEnabler library is able to obtain such individualization information and to make it available to the Adobe Pass authentication services during the entitlement calls. The service will use this information and embed it in the actual tokens, thus effectively binding the tokens to a specific device. The end goal of this is to make the tokens non-transferable across devices.

In the XML listings above, note the tag entitled simpleTokenFingerprint. The purpose of this tag is to hold native device ID individualization info. The AccessEnabler library is able to obtain such individualization information and to make it available to the Adobe Pass authentication services during the entitlement calls. The service will use this information and embed it in the actual tokens, thus effectively binding the tokens to a specific device. The end goal of this is to make the tokens non-transferable across devices.

Since this is obviously a security related feature, this information is inherently "sensitive" from the security point of view. As a result, this information needs to be protected against both tampering and eavesdropping. The eavesdropping issue is solved by sending the authentication/authorization requests over the HTTPS protocol. The tampering protection is handled by digitally signing the device identification information. The AccessEnabler library computes a device ID from information provided by the device, then sends the device ID "in the clear" to the Adobe Pass authentication servers as a request parameter.  The Adobe Pass authentication servers digitally sign the device ID with Adobe's private key and add it to the authentication token that is returned to the AccessEnabler. Thus the device ID is bound with the authentication token.  During the authorization flow, the AccessEnabler again sends the device ID in the clear, along with the authentication token.  Failure of the validation process will automatically lead to failure of the authentication/authorization workflows.  The Adobe Pass authentication servers apply the private key to the device ID and compare it to the value in the authentication token.  If they don't match, that entitlement flow fails.
