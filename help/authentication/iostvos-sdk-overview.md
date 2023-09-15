---
title: iOS/tvOS SDK Overview
description: iOS/tvOS SDK Overview
exl-id: b02a6234-d763-46c0-bc69-9cfd65917a19
---
# iOS/tvOS SDK Overview {#iostvos-sdk-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


</br>


## Introduction {#intro}

iOS AccessEnabler is an Objective C iOS/tvOS library that enables mobile apps to use Adobe Pass authentication for TV Everywhere's entitlement services. The implementation consists of the *AccessEnabler* interface that defines the entitlement API, and the *EntitlementDelegate* and *[EntitlementStatus](#ios%20entitlement%20status)* protocols that describes the callbacks that the library triggers. The interface together with the protocol is referred to under one common name: the AccessEnabler library.

## iOS and tvOS Requirements {#reqs}

For current technical requirements related to the iOS and tvOS platform and Adobe Pass Authentication, see [Platform / Device / Tool Requirements](#ios), and consult the release notes included with the SDK download. Throughout the rest of this page, you will see sections that note changes that apply to particular SDK versions and higher. For example, the following is a legitimate note regarding the 1.7.5 SDK:

## Understanding Native Client Workflows {#flows}

Native client workflows are typically the same as or very similar to those of browser-based Adobe Pass authentication clients. However, there are a few exceptions, as described below.

- [Post-initialization Workflow](#post-init)
- [Generic Initial Authentication Workflow](#generic)
- [Logout Workflow](#logout)


### Post-initialization Workflow {#post-init}

All of the entitlement workflows supported by the AccessEnabler assume that you have previously called [`setRequestor()`](#setReq) to establish your identity. You make this call to provide your Requestor ID only once, usually during your application's initialization/setup phase.

  
With an iOS native client, after your initial call to [`setRequestor()`](#setReq), you have a choice as to how to proceed:

- You can start making entitlement calls immediately and allow them to be queued silently, if needed.

- You can receive a confirmation of the success/failure of [`setRequestor()`](#setReq) by implementing the [`setRequestorComplete()`](#setReqComplete) callback.

- You can do both of the above.

It is your choice to either have your app wait for notification of the success of [`setRequestor()`](#setReq) or have it rely on the AccessEnabler's call queue mechanism. Since all subsequent authorization and authentication requests need the requestor ID and the associated configuration information, the [`setRequestor()`](#setReq) method effectively blocks all authentication and authorization API calls until initialization is complete.

 

### Generic Initial Authentication Workflow {#generic}

The purpose of this workflow is to log in a user with their MVPD. After a successful login, the backend server issues the user an authentication token. While authentication is typically done as part of the authorization process, the following describes how authentication can work in isolation, and does not include any authorization steps.

Note that while this workflow differs for native clients from the typical browser-based authentication workflow, steps 1-5 are the same for both native clients and browser-based clients.

1.  Your application initiates the authentication workflow with a call to AccessEnabler's `getAuthentication() `API method, which checks for a valid cached authentication token.
1.  If the user is currently authenticated, the AccessEnabler calls your [`setAuthenticationStatus()`](#setAuthNStatus) callback function, passing an authentication status indicating success, and ending the flow.
1.  If the user is not currently authenticated, the AccessEnabler continues the authentication flow by determining whether the user's last authentication attempt was successful with a given MVPD. If an MVPD ID is cached AND the `canAuthenticate` flag is true OR an MVPD was selected using [`setSelectedProvider()`](#setSelProv), the user is not prompted with the MVPD selection dialog. The authentication flow continues using the cached value of the MVPD (that is, the same MVPD that was used during the last successful authentication). A network call is made to the backend server, and the user is redirected to the MVPD login page (Step 6 below).
1.  If no MVPD ID is cached AND no MVPD was selected using [`setSelectedProvider()`](#setSelProv) OR the `canAuthenticate` flag is set to false, the [`displayProviderDialog()`](#dispProvDialog) callback is called. This callback instructs your application to create the UI that presents the user a list of MVPDs to choose from. An array of MVPD objects is provided, containing the necessary information for you to build the MVPD selector. Each MVPD object describes an MVPD entity, and contains information such as the ID of the MVPD (e.g., XFINITY, AT\&T, etc.) and the URL where the MVPD logo can be found.
1.  Once a particular MVPD is selected, your application must inform the AccessEnabler of the user's choice. Once the user selects the desired MVPD, you inform the AccessEnabler of the user selection via a call to the [`setSelectedProvider()`](#setSelProv) method.
1.  The iOS AccessEnabler calls your `navigateToUrl:` callback or `navigateToUrl:useSVC:` callback to redirect the user to the MVPD login page. By triggering either one, the AccessEnabler makes a request to your application to create a `UIWebView/WKWebView or SFSafariViewController` controller and to load the URL provided in the callback's `url` parameter. This is the URL of the authentication endpoint on the backend server. For tvOS AccessEnabler, the [status()](#status_callback_implementation) callback is called with a `statusDictionary` parameter and the polling for the second screen authentication is immediately started. The `statusDictionary` contains the `registration code` that needs to be used for the second screen authentication. 
1.  In case of the iOS AccessEnabler, the user lands on the MVPD's login page to input his credentials through the medium of your application `UIWebView/WKWebView or SFSafariViewController `controller. Note that several redirect operations occur during this transfer and your application must monitor the URLs that are loaded by the controller during the multiple redirect operations.
1.  In case of the iOS AccessEnabler, when the `UIWebView/WKWebView or SFSafariViewController` controller loads a specific custom URL your application must close the controller and call AccessEnabler's `handleExternalURL:url `API method. Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the authentication flow has completed and that it is safe to close the `UIWebView/WKWebView or SFSafariViewController` controller. In case your application is required to use a `SFSafariViewController `controller the specifc custom URL is defined by the `application's custom scheme` (e.g.: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the `ADOBEPASS_REDIRECT_URL` constant (i.e. `adobepass://ios.app`).
1.  Once your application closes the `UIWebView/WKWebView or SFSafariViewController` controller and calls AccessEnabler's `handleExternalURL:url `API method, the AccessEnabler retrieves the authentication token from the backend server and informs your application that the authentication flow is complete. The AccessEnabler calls the [`setAuthenticationStatus()`](#setAuthNStatus) callback with a status code of 1, indicating success. If there is an error during the execution of these steps, the [`setAuthenticationStatus()`](#setAuthNStatus) callback is triggered with a status code of 0, indicating authentication failure, as well as a corresponding error code.


>[!WARNING]
>
> During the steps where the AccessEnabler relinquishes control to your app (i.e., when the provider selection dialog is displayed, or when the UIWebView/WKWebView or SFSafariViewController is displayed) the user has the opportunity to cancel the authentication flow. In these situations, your app is responsible for informing the AccessEnabler about this event and calling the [`setSelectedProvider()`](#setSelProv) API method, passing null as a parameter. This gives the AccessEnabler a chance to clean up its internal state and reset the authentication flow. On tvOS, you can use the same method to cancel the authentication polling.


### Logout Workflow {#logout}

For native clients, logout is handled similarly to the authentication process described above.

1.  Your application initiates the logout workflow with a call to AccessEnabler's `logout() `API method. The logout is the result of a series of HTTP redirect operations due to the fact that the user needs to be logged out from both Adobe Pass Authentication servers and also from the MVPD's servers. Because this flow cannot be completed with a simple HTTP request issued by the AccessEnabler library, a `UIWebView/WKWebView or SFSafariViewController` controller needs to be instantiated in order to be able to follow the HTTP redirect operations.

1.  A pattern similar with the authentication flow is employed. The iOS AccessEnabler triggers the `navigateToUrl:` callback or the `navigateToUrl:useSVC:` to create a `UIWebView/WKWebView or SFSafariViewController` controller and to load the URL provided in the callback's `url` parameter. This is the URL of the logout endpoint on the backend server. For the tvOS AccessEnabler neither the `navigateToUrl:` callback or the `navigateToUrl:useSVC:` callback is called.

1.  As it goes through several redirects, your application must monitor the activity of the `UIWebView/WKWebView or SFSafariViewController `controller and detect the moment when it loads a specific custom URL. Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the logout flow has completed and that it is safe to close the controller. When the controller loads this specific custom URL your application must close the controller and call AccessEnabler's `handleExternalURL:url `API method. In case your application is required to use a `SFSafariViewController `controller the specifc custom URL is defined by the `application's custom scheme` (e.g.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the ` ADOBEPASS_REDIRECT_URL  `constant (i.e. `adobepass://ios.app`).

1.  In the end the AccessEnabler will call the [`setAuthenticationStatus()`](#setAuthNStatus) callback with a status code of 0, indicating success of the logout flow.

The logout flow differs from the authentication flow in that the user is not required to interact with the `UIWebView/WKWebView or SFSafariViewController`  controller in any way. Therefore, Adobe recommends that you make the control invisible (i.e. hidden) during the logout process.

## Tokens {#tokens}

- [Definitions and Usage](#definitions)
- [Caching Guidelines](#caching)
- [Persistence](#persistence)
- [Format](#format)
- [Device Binding](#device_binding)


### Definitions and Usage {#definitions}

The Adobe Pass authentication entitlement solution revolves around the generation of specific pieces of data (tokens) that Adobe Pass authentication generates upon the successful completion of the authentication and authorization workflows. These tokens are stored locally on the client's iOS device.

 

Tokens have a limited lifespan; upon expiration, tokens need to be re-issued through the re-initiation of the authentication and / or authorization workflows.

 

There are three types of tokens issued during the entitlement workflows:

- **Authentication token:** The end result of the user authentication workflow will be an authentication GUID that the AccessEnabler can use to make authorization queries on the user's behalf. This authentication GUID will have an associated time-to-live (TTL) value which may be different from the user's authentication session itself. An authentication token will be generated by binding the authentication GUID to the device initiating the authentication requests.
- **Authorization token:** Grants access to a specific protected resource identified by a unique resourceID. It consists of an authorization grant issued by the authorizing party along with the original resourceID. This information is bound to the device initiating the request.
- **Short-lived media token:** The AccessEnabler grants access to the hosting application for a given resource by returning a short-lived media token. This token is generated based on the authorization token that was previously acquired for that specific particular resource. Also, this token is not bound to the device and the associated life-span is significantly shorter (default: 5 minutes).

Upon successful authentication and authorization, Adobe Pass authentication will issue authentication, authorization and short-lived media tokens. These tokens should be cached on the user's device and used for the duration of their associated life-spans.

 

### Caching Guidelines {#caching}

- Authentication Token
- Authorization Token
- Short-lived Media Token


#### Authentication Token

- **AccessEnabler 1.7:** This SDK introduces a new method of token storage, enabling multiple Programmer-MVPD buckets, and therefore, multiple authentication tokens. Now, the same storage layout is used for both the "Authentication per Requestor" scenario and for the normal authentication flow. The only difference between the two is in the way authentication is performed: "Authentication per Requestor" contains a new improvement (Passive Authentication) that makes it possible for the AccessEnabler to perform back-channel authentication, based on the existence of an authentication token in the storage (for a different Programmer). The user only has to authenticate once, and this session will be used to obtain authentication tokens in additional apps. This back-channel flow takes place during the [`setRequestor()`](#setReq) call and is mostly transparent to the Programmer. **There is, however, one important requirement here: the Programmer MUST call setRequestor() from the main UI thread.**
- **AccessEnabler 1.6 and older:** The way in which authentication tokens are cached on the device depends on the "**Authentication per Requestor"** flag associated with the current MVPD:

<!-- end list -->

1.  If the "Authentication per Requestor" feature is disabled, then a single authentication token will be stored locally in the global pasteboard; this token will be shared between all applications that are integrated with the current MVPD.
1.  If the "Authentication per Requestor" feature is enabled, then a token will be explicitly associated with the Programmer that performed the authentication flow (the token will not be stored in the global pasteboard, but in a private file visisble only to that Programmer's application). More specifically, Single Sign-On (SSO) between different applications will be disabled; the user will need to perform the authentication flow explicitly when switching to a new app (providing the fact that the Programmer of the second app is integrated with the current MVPD and that no authentication token exists for that Programmer in the local cache).

 

#### Authorization Token

At any given moment only ONE authorization token PER RESOURCE gets cached by the AccessEnabler. There can be multiple authorization tokens cached but they are associated with different resources. Whenever a new authorization token is issued and an old one already exists for *the same resource*, the new token overwrites the existing cached value.

 

#### Media Token

The short-lived media token should NOT be cached at all. The media token should be retrieved from the server every time an authorization API is called, because it is restricted to one-time use.

 

### Persistence {#persistence}

Tokens need to be persistent across consecutive runs of the same application. This means that once the authentication and authorization tokens have been acquired and the user closes the application, the same tokens are available to the application when the user re-opens the application. Moreover, it is desirable that these tokens be persistent across multiple applications. In other words, after a user uses one application to login with a specific identity provider (successfully obtaining authentication and authorization tokens), the same tokens can be used through a different application, and the user is no longer prompted for credentials when logging in via the same identity provider. This type of seamless authentication / authorization workflow is what makes the Adobe Pass authentication solution a true TV-Everywhere
implementation. 

 

## iOS

The iOS AccessEnabler library works around the issues of cross-application data sharing by storing the token data into a "clipboard-like" data structure called the *paste board*. This system-level shared resource provides the key ingredients that enable the implementation of the desired persistent tokens use case:

- **Support for structured storage** - The paste board is not just a simple, linear buffer-like memory structure. It provides a dictionary-like storage mechanism that allows for data indexing based on user-specified key values.
- **Support for data persistence using the underlying file system** - The contents of the paste board structure can be marked as persistent, in which case the data is saved on the device's internal memory.

 

Once a particular token is placed into the token cache, its validity will be checked at different times by the AccessEnabler library.  A valid token is defined as:

- The token's TTL has not expired.
- The issuer of the token is included in the list of allowed identity providers.

 

## tvOS

Since on tvOS the pasteboard is not available, the tvOS AccessEnabler library uses the NsUserDefaults as a storage option. This solves the problem of persisting authentication and authorization tokens but the information stored cannot be shared among different applications.

 

**iOS 10 Pasteboard Changes -** When upgrading from a previous version of iOS, the pasteboard will be erased. This means that all applications need to be re-authenticated.

 

**iOS 7 Pasteboard Changes -** Due to changes in how pasteboards function on iOS 7, there will be limited Cross SSO between applications running on iOS 7. Applications having the same `<Bundle Seed ID>`(also known as `<Team ID>`) will share tokens, meaning that apps A1 and A2 from the same Programmer X will share tokens, while app A1 (Programmer X) and app A3 (Programmer Y) will not share tokens. 

- Bundle Seed ID/Team ID is the same between 2 apps if they are generated by the same Provisioning Profile. Find more information at this link:
  [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- This "Cross SSO" limitation will be present in iOS 7 regardless of the Adobe Pass authentication SDK used. 

Please read this tech note for more information on configuring SSO on iOS 7 and upper (the tech note applies for Access Enabler v1.8 and upper): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### Token Storage (AccessEnabler 1.7)

Starting with AccessEnabler 1.7, the token storage can support multiple Programmer-MVPD combinations, relying on a multi-level nested map structure that can hold multiple authentication tokens. This new storage does not affect the AccessEnabler public API in any way and does not require changes on the Programmer's side. Here is an example that
illustrates this new functionality:

1.  Open App1 (developed by Programmer1).
1.  Authenticate with MVPD1 (which is integrated with Programmer1).
1.  Suspend / Close the current application, and open App2 (developed by Programmer2).
1.  Let's assume that Programmer2 is not integrated with MVPD2; therefore, the user will NOT be authenticated in App2.
1.  Authenticate with MVPD2 (which is integrated with Programmer2) in App2.
1.  Switch back to App1; the user will still be authenticated with Programmer1.

In older versions of the AccessEnabler, Step 6 would render the user as not-authenticated, because the token storage formerly supported only one authentication token.

 

Logging out from one Programmer / MVPD session will clear the entire underlying storage, including all of the other Programmer / MVPD authentication tokens on the device. On the other hand, canceling the authentication flow (invoking [`setSelectedProvider(null)`](#setSelProv)) will NOT clear the underlying storage, but it will only affect the current Programmer / MVPD authentication attempt (by erasing the MVPD for the current Programmer).

 

### Token Importer  (AccessEnabler 1.7)

Another storage-related feature that is included in AccessEnabler 1.7 makes it possible to import authentication tokens from older storage areas. This "Token Importer" helps to achieve compatibility between consecutive AccessEnabler releases, maintaining the SSO state even when the storage version is upgraded. The importer is executed during the [`setRequestor()`](#setReq) flow and runs in the following two scenarios (assuming that no valid authentication token for the current Programmer is present in the current storage):

- The first install of a 1.7 app developed by a specific Programmer
- Upgrade path to a future AccessEnabler that uses a new storage

The import operation is transparent to the Programmer and does not require any code change in the client application.

 

### Token Sanitizer  (AccessEnabler 1.7.5)

From AccessEnabler 1.7.5 forward, this service runs on [`setRequestor()`](#setReq)`. `It was developed as a result of the iOS 7 switch from the WiFi MAC address to the IDFA for tracking. The sanitizer ensures that the current storage contains only valid authentication tokens (valid in terms of the Device ID, formerly calculated using the MAC address, prior to iOS7). The Token Sanitizer removes all invalid tokens. 

 

The Token Sanitizer service is most useful when an AccessEnabler 1.7.5 application is used on iOS 6, and then the user updates to iOS 7. When this happens, all of the authentication tokens that were obtained on iOS 6 will now be invalid (because of the Device ID algorithm change from using the MAC address to the IDFA). The sanitizer will clear all of the invalid tokens, and the user will then be unauthenticated. 

 

Without the Token Sanitizer removing invalid tokens, the AccessEnabler would fail to obtain authorizations due to the presence of invalid authentication tokens. This would prove tricky for the end-user to debug, since authorization error messages can be cryptic and not overly helpful in determining what caused the problem. 

 

### Format {#format}

- [AuthN Token](#authn_token)
- [AuthZ Token](#authz_token)
- [Short Media Token](#short_token)
- [Device Binding](#device_binding)


Note that the format of the AuthN and AuthZ tokens are included here for background information only. The structure of these tokens could be changed by Adobe Pass authentication at any time. Programmers don't need to know the exact structure of the AuthN and AuthZ tokens to implement their apps, as the AuthN and AuthZ tokens are not exposed on the local device. The Short Media token *is* exposed to the Programmer's application.

 

#### Authentication Token {#authn_token}

The listing below presents the format of the authentication token:

```
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

```
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
 

#### Short Media Token {#short_token}

The listing below presents the format of the short media token. This token is exposed to the Programmer's application. It is pased to the Programmer's application at the end of a successful entitlement process:

```
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
 

### Device Binding {#device_binding}

In the XML listings above, note the tag entitled `simpleTokenFingerprint`. The purpose of this tag is to hold native device ID individualization info. The AccessEnabler library is able to obtain such individualization information and to make it available to the Adobe Pass authentication services during the entitlement calls. The service will use this information and embed it in the actual tokens, thus effectively binding the tokens to a specific device. The end goal of this is to make the tokens non-transferable across devices.

 

Since this is obviously a security related feature, this information is inherently "sensitive" from the security point of view. As a result, this information needs to be protected against both tampering and eavesdropping. The eavesdropping issue is solved by sending the authentication/authorization requests over the HTTPS protocol. The tampering protection is handled by digitally signing the device identification information. The AccessEnabler library computes a device ID from information provided by the device, then sends the device ID "in the clear" to the Adobe Pass authentication servers as a request parameter. The Adobe Pass authentication servers digitally sign the device ID with Adobe's private key and add it to the authentication token that is returned to the AccessEnabler. Thus the device ID is bound with the authentication token. During the authorization flow, the AccessEnabler again sends the device ID in the clear, along with the authentication token. Failure of the validation process will automatically lead to failure of the authentication / authorization workflows. The Adobe Pass authentication servers apply the private key to the device ID and compare it to the value in the authentication token. If they don't match, that entitlement flow fails.

 

**Note on Device Binding in AccessEnabler 1.7.5:** Beginning with AccessEnabler 1.7.5, there is a change in how the device ID is calculated to provide individualization information for an iOS device. This change reflects a change in iOS 7: From iOS 7, Apple no longer provides the WiFi MAC address as a tracking option, in favor of its Identifier for Advertisers (IDFA). Since individualization information for an app running on iOS 7 is based on the IDFA, and that info is embedded in the entitlement flow tokens, this means that there are a number of different possible effects on user experience that result from this change. The different possible effects are based on which version of iOS the user is upgrading from combined with which version of the AccessEnabler the Programmer is upgrading from. For details on this change, see the Release notes included with AccessEnabler SDK 1.7.5.

<!--
## Related Information {#related}


- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Pass
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Adobe Pass authentication Access
  Enabler](#)
-->
