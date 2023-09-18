---
title: Android SDK Overview
description: Android SDK Overview
exl-id: a1d98325-32a1-4881-8635-9a3c38169422
---
# Android SDK Overview {#android-sdk-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>


## Introduction {#intro}

Android AccessEnabler is a Java Android library that enables mobile apps to use Adobe Pass Authentication for TV Everywhere's entitlement services. An Android implementation consists of the AccessEnabler interface that defines the entitlement API, and an EntitlementDelegate protocol that describes the callbacks that the library triggers. The interface together with the protocol is referred to under one common name: the AccessEnabler Android library.

## Android Requirements {#reqs}

For current technical requirements related to the Android platform and Adobe Pass Authentication, see [Platform / Device / Tool Requirements](#android), or consult the release notes included with the Android SDK download.

## Understanding Native Client Workflows {#native_client_workflows}

Native client workflows are typically the same as, or very similar to, those of browser-based Adobe Pass Authentication clients. However, there are a few exceptions, as described below.

- [Post-initialization Workflow](#post-init)
- [Generic Initial Authentication Workflow](#generic)
- [Logout Workflow](#logout)



### Post-initialization Workflow {#post-init}

All of the entitlement workflows supported by the AccessEnabler assume that you have previously called [`setRequestor()`](#setRequestor) to establish your identity. You make this call to provide your Requestor ID only once, usually during your application's initialization/setup phase.

  
With the native clients (e.g., Android), after your initial call to [`setRequestor()`](#setRequestor), you have a choice as to how to proceed:

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
1.  For Android applications, if com.android.chrome is available, the authentication url will be loaded in Chrome Custom Tabs.
1.  Via Chrome Custom Tabs, the user arrives on the MVPD's login page and inputs their credentials. Note that several redirect operations occur during this transfer.
1.  When Chrome Custom Tabs detect that an url matches the scheme (adobepass://) and deep link from resource "redirect\_uri" (i.e., adobepass://com.adobepass ), the AccessEnabler retrieves the actual authentication token from the backend servers. Note that the final redirect URLs are actually invalid, and they are not intended for Chrome Custom Tabs to actually load them. They must only be interpreted by the SDK as a signal that the authentication flow has completed.
1.  The AccessEnabler informs your application that the authentication flow is complete. The AccessEnabler calls the [`setAuthenticationStatus()`](#setAuthNStatus) callback with a status code of 1, indicating success. If there is an error during the execution of these steps, the [`setAuthenticationStatus()`](#setAuthNStatus) callback is triggered with a status code of 0, along with a corresponding error code, indicating authentication failure.

### Logout Workflow {#logout}

For native clients, logouts are handled similarly to the authentication process described above. Following this pattern, the AccessEnabler open Chrome Custom Tabs and load the URL of the logout endpoint on the backend server.



**Note:** Logging out from one Programmer / MVPD session will clear
the underlying storage for that specific MVPD including all of the
other Programmer authentication tokens obtained through SSO on
that device. Tokens obtained for other MVPDs or not thru SSO will not
be deleted. 


## Tokens {#tokens}

- [Definitions and Usage](#definitions)
- [Caching Guidelines](#caching)
- [Persistence](#persistence)
- [Format](#format)
- [Device Binding](#device_binding)



### Definitions and Usage {#definitions}

The Adobe Pass Authentication entitlement solution revolves around the generation of specific pieces of data (tokens) that Adobe Pass Authentication generates upon the successful completion of the authentication and authorization workflows. These tokens are stored locally on the client's Android device.

Tokens have a limited lifespan; upon expiration, tokens need to be re-issued through the re-initiation of the authentication and/or authorization workflows.

There are three types of tokens issued during the entitlement workflows:

- **Authentication token** - The end result of the user authentication workflow will be an authentication GUID that the AccessEnabler can use to make authorization queries on the user's behalf. This authentication GUID will have an associated time-to-live (TTL) value which may be different from the user's authentication session itself. Adobe Pass Authentication generates an authentication token by binding the authentication GUID to the device initiating the authentication requests.
- **Authorization token** - Grants access to a specific protected resource identified by a unique `resourceID`. It consists of an authorization grant issued by the authorizing party along with the original `resourceID`. This information is bound to the device initiating the request.
- **Short-lived media token** - The AccessEnabler grants access to the hosting application for a given resource by returning a short-lived Media Token. This token is generated based on the authorization token that was previously acquired for that specific particular resource. Also, this token is not bound to the device, and the associated life-span is significantly shorter (default: 5 minutes).

Upon successful authentication and authorization, Adobe Pass Authentication will issue authentication, authorization and short-lived media tokens. These tokens should be cached on the user's device and used for the duration of their associated life-spans.



### Caching Guidelines {#caching}

- Authentication Token
- Authorization Token
- Media Token


#### Authentication Token

- **AccessEnabler 1.6 and older** - The way in which authentication tokens are cached on the device depends on the "**Authentication per Requestor"** flag associated with the current MVPD:


1.  If the "Authentication per Requestor" feature is *disabled*, then a single authentication token will be stored locally in the global pasteboard. This token will be shared between all applications that are integrated with the current MVPD.
1.  If the "Authentication per Requestor" feature is *enabled*, then a token will be explicitly associated with the Programmer that performed the authentication flow (the token will not be stored in the global pasteboard, but in a private file visisble only to that Programmer's application). More specifically, Single Sign-On (SSO) between different applications will be disabled; the user will need to perform the authentication flow explicitly when switching to a new app (providing that the Programmer of the second app is integrated with the current MVPD and that no authentication token exists for that Programmer in the local cache).

    **Note:** AE 1.6 Google GSON Tech Note: [How to resolve Gson dependencies](https://tve.zendesk.com/entries/22902516-Android-AccessEnabler-1-6-How-to-resolve-Gson-dependencies)

- **AccessEnabler 1.7** - This SDK introduces a new method of token storage, enabling multiple Programmer-MVPD buckets, and therefore, multiple authentication tokens. From AE 1.7, the same storage layout is used for both the "Authentication per Requestor" scenario and for the normal authentication flow. The only difference between the two is in the way authentication is performed: "Authentication per Requestor" contains a new improvement (passive authentication) that makes it possible for the AccessEnabler to perform back-channel authentication, based on the existence of an authentication token in the storage (for a different Programmer). The user only has to authenthenticate once, and this session will be used to obtain authentication tokens in subsequent apps. This back-channel flow takes place during the [`setRequestor()`](#setRequestor) call and is mostly transparent to the Programmer. There is however one important requirement here: the Programmer MUST call [`setRequestor()`](#setRequestor) from the main UI thread and from within an Activity. 


#### Authorization Token

At any given moment only ONE authorization token per resource gets cached by the AccessEnabler. There can be multiple authorization tokens cached, but they are associated with different resources. Whenever a new authorization token is issued and an old one already exists for the same resource, the new token overwrites the existing cached value.



#### Media Token 

The short-lived media token should NOT be cached at all. The media token should be retrieved from the server every time an authorization API is called, because it is restricted to one-time use.



### Persistence {#persistence}

Tokens need to be persistent across consecutive runs of the same application. This means that once the authentication and authorization tokens have been acquired and the user closes the application, the same tokens are available to the application when the user re-opens the application. Moreover, it is desirable that these tokens be persistent across multiple applications. In other words, after a user uses one application to login with a specific identity provider (successfully obtaining authentication and authorization tokens), the same tokens can be used through a different application, and the user is no longer prompted for credentials when logging in via the same identity provider.



This type of seamless authentication / authorization workflow is what makes the Adobe Pass Authentication solution a true TV-Everywhere implementation. From a pure engineering point of view, the Android AccessEnabler library works around the issues of cross-application data sharing by storing the token data into a database file located on external storage. This system-level shared resources provides the key ingredients that enable the implementation of the desired persistent tokens use-case:

- Support for structured storage - The Adobe Pass Authentication token storage is not just a simple linear buffer-like memory structure. It provides a dictionary-like storage mechanism that allows for data indexing based on user-specified key values.
- Support for data persistence using the underlying file system - The contents of the database file are persisted by default and the data is saved on the device's external memory.



Once a particular token is placed into the token cache, its validity will be checked at different times by the AccessEnabler library.  A valid token is defined as:

- The token's TTL has not expired
- The issuer of the token is included in the list of allowed identity providers



Starting with AccessEnabler 1.7, the token storage can support multiple Programmer-MVPD combinations, relying on a multi-level nested map structure that can hold multiple authentication tokens. This new storage does not affect the AccessEnabler public API in any way and does not require changes on the Programmer's side. Here is an example that illustrates this newer functionality:

1.  Open App1 (developed by Programmer1).
1.  Authenticate with MVPD1 (which is integrated with Programmer1).
1.  Suspend / Close the current application, and open App2 (developed by Programmer2).
1.  Let's assume that Programmer2 is not integrated with MVPD2; therefore, the user will NOT be authenticated in App2.
1.  Authenticate with MVPD2 (which is integrated with Programmer2) in App2.
1.  Switch back to App1; the user will still be authenticated with Programmer1.

In older versions of the AccessEnabler, Step 6 would render the user as not-authenticated, because the token storage formerly supported only one authentication token.


**NOTE:** Logging out from one Programmer / MVPD session will clear the underlying storage, including all of the other Programmer authentication tokens on the device with SSO. Tokens obtained for other MVPDs or not thru SSO will not be deleted. Canceling the authentication flow (invoking [`setSelectedProvider(null)`](#setSelectedProvider)) will NOT clear the underlying storage, but will only affect the current Programmer / MVPD authentication attempt (by erasing the MVPD for the current Programmer).


Another storage-related feature that is included in AccessEnabler 1.7 makes it possible to import authentication tokens from older storage areas. This "Token Importer" helps to achieve compatibility between consecutive AccessEnabler releases, maintaining the SSO state even when the storage version is upgraded. 

The importer is executed during the [`setRequestor()`](#setRequestor) flow, and runs in the following two scenarios (assuming that no valid authentication token for the current Programmer is present in the current storage):

- The first install of a 1.7 app developed by a specific Programmer
- Upgrade path to a future AccessEnabler that use a new storage

The import operation is transparent to the Programmer and does not require any code change in the client application.



### Format {#format}

- [Authentication Token](#authn_token)
- [Authorization Token](#authz_token)
- [Short Media Token](#short_media_token)
- [Device Binding](#device_binding)

#### Authentication Token {#authn_token}

The listing below presents the format of the authentication token:

```XML
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

```XML
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

```XML
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

In the XML listings above, note the tag entitled `simpleTokenFingerprint`. The purpose of this tag is to hold native device ID individualization info. The AccessEnabler library is able to obtain such individualization information and to make it available to the Adobe Pass Authentication services during the entitlement calls. The service will use this information and embed it in the actual tokens, thus effectively binding the tokens to a specific device. The end goal of this is to make the tokens non-transferable across devices.



In the XML listings above, note the tag entitled simpleTokenFingerprint. The purpose of this tag is to hold native device ID individualization info. The AccessEnabler library is able to obtain such individualization information and to make it available to the Adobe Pass Authentication services during the entitlement calls. The service will use this information and embed it in the actual tokens, thus effectively binding the tokens to a specific device. The end goal of this is to make the tokens non-transferable across devices.



Since this is obviously a security related feature, this information is inherently "sensitive" from the security point of view. As a result, this information needs to be protected against both tampering and eavesdropping. The eavesdropping issue is solved by sending the authentication/authorization requests over the HTTPS protocol. The tampering protection is handled by digitally signing the device identification information. The AccessEnabler library computes a device ID from information provided by the device, then sends the device ID "in the clear" to the Adobe Pass Authentication servers as a request parameter.  The Adobe Pass Authentication servers digitally sign the device ID with Adobe's private key and add it to the authentication token that is returned to the AccessEnabler. Thus the device ID is bound with the authentication token.  During the authorization flow, the AccessEnabler again sends the device ID in the clear, along with the authentication token.  Failure of the validation process will automatically lead to failure of the authentication/authorization workflows.  The Adobe Pass Authentication servers apply the private key to the device ID and compare it to the value in the authentication token.  If they don't match, that entitlement flow fails.


<!--
## Related Information {#related}

- [Android Integration Cookbook](#)
- [Android API](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Pass Authentication native SDK (Tech Note)](#)
- [AE 1.6: How to resolve Gson dependencies (Tech Note)](#)
-->
