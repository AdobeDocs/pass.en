---
title: iOS/tvOS Cookbook
description: iOS/tvOS Cookbook
exl-id: 4743521e-d323-4d1d-ad24-773127cfbe42
---
# (Legacy) iOS/tvOS SDK Cookbook {#iostvos-sdk-cookbook}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Introduction {#intro}

This document describes the entitlement workflows that a Programmer's upper-level application can implement through the APIs exposed by the iOS/tvOS AccessEnabler library.

The Adobe Pass Authentication entitlement solution for iOS/tvOS is ultimately divided into two domains:

*   The UI domain - this is the upper-level application layer which implements the UI and uses the services provided by the AccessEnabler library to provide access to restricted content.

*   The AccessEnabler domain - this is where the entitlement workflows are implemented in the form of:

    * Network calls made to Adobe's backend servers
    * Business-logic rules related to the authentication and authorization workflows
    * Management of various resources and processing of workflow state (such as the token cache)

The goal of the AccessEnabler domain is to hide all the complexities of the entitlement workflows, and provide to the upper-layer application (through the AccessEnabler library) a set of simple entitlement primitives with which you implement the entitlement workflows:

1. Set the requestor identity
1. Check and get authentication against a particular identity provider
1. Check and get authorization for a particular resource
1. Logout
1. Apple SSO flows by proxing the Apple VSA framework

The AccessEnabler's network activity takes place in its own thread, so the UI thread is never blocked. As a result, the two-way communication channel between the two application domains must follow a fully asynchronous pattern:

* The UI application layer sends messages to the AccessEnabler domain via the API calls exposed by the AccessEnabler library.
* The AccessEnabler responds to the UI layer through the callback methods included in the AccessEnabler protocol which the UI layer registers with the AccessEnabler library.

## Configuring the Experience Cloud ID Service (Visitor ID) {#visitorIDSetup}

Configuring the [Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html) value is important from the [!DNL Analytics] point of view. Once a `visitorID` value is set, the SDK sends this information along with every netwrok call and the [!DNL Adobe Pass] Authentication server collects this information. You can correlate the analytics from Adobe Pass Authentication service with any other anayltics reports that you may have from other applications or websites. Information on how to setup visitorID can be found [here](#setOptions).

## Entitlement Flows {#entitlement}

A.  [Prerequisites](#prereqs) </br>
B.  [Startup Flow](#startup_flow) </br>
C.  [Authentication Flow withouth Apple SSO](#authn_flow_wo_applesso)  </br>
D.  [Authentication Flow with Apple SSO on iOS](#authn_flow_with_applesso) </br>
E.  [Authentication Flow with Apple SSO on tvOS](#authn_flow_with_applesso_tvOS) </br>
F.  [Authorization Flow](#authz_flow) </br>
G.  [View Media Flow](#media_flow) </br>
H.  [Logout Flow without Apple SSO](#logout_flow_wo_AppleSSO) </br>
I.  [Logout Flow with Apple SSO](#logout_flow_with_AppleSSO) </br>


### A. Prerequisites {#prereqs}

1.  Create your callback functions:
    *   `setRequestorComplete()` </br>
      * Triggered by [setRequestor()](#$setReq), returns success or failure. </br>
      * Success indicates you can proceed with entitlement calls.

    * [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      * Triggered by [`getAuthentication()`](#$getAuthN) only if the user has not selected a provider (MVPD) and is not yet authenticated. </br>
      * The `mvpds` parameter is an array of providers available to the user.

    * `setAuthenticationStatus(status, errorcode)` </br>
      * Triggered by `checkAuthentication()` every time. </br>
      * Triggered by [`getAuthentication()`](#$getAuthN) only if the user is already authenticated and has selected a provider. </br>
      * Status returned is success or failure, the errorcode describes the type of the failure.

    * [`navigateToUrl(url)`](#$nav2url) </br>
      * Triggered by [`getAuthentication()`](#$getAuthN) after the user selects an MVPD. The `url` parameter provides the location of the MVPD's login page.

    * `sendTrackingData(event, data)` </br>
      * Triggered by `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.  
      * The `event` parameter indicates which entitlement event occurred; the `data` parameter is a list of values relating to the event. 

    * `setToken(token, resource)`

      * Triggered by [checkAuthorization()](#checkAuthZ) and [getAuthorization()](#$getAuthZ) after a successful authorization to view a resource.  
      * The `token` parameter is the short-lived media token; the `resource` parameter is the content that the user is authorized to view.

    * `tokenRequestFailed(resource, code, description)` </br>
      * Triggered by [checkAuthorization()](#checkAuthZ) and [getAuthorization()](#$getAuthZ) after an unsuccessful authorization.  
      * The `resource` parameter is the content that the user was attempting to view; the `code` parameter is the error code indicating what type of failure occurred; the `description` parameter describes the error associated with the error code.

    * `selectedProvider(mvpd)` </br>
      * Triggered by [`getSelectedProvider()`](#getSelProv).  
      * The `mvpd` parameter provides information about the provider selected by the user.

    * `setMetadataStatus(metadata, key, arguments)`
      * Triggered by `getMetadata().`  
      * The `metadata` parameter provides the specific data you requested; the `key` parameter is the key used in the [getMetadata()](#getMeta) request; and the `arguments` parameter is the same dictionary that was passed to [getMetadata()](#getMeta).

    * [`preauthorizedResources(authorizedResources)`](#preauthResources)

      * Triggered by [`checkPreauthorizedResources()`](#checkPreauth).

      * The `authorizedResources` parameter presents the resources that the user
is authorized to view.

    * [`presentTvProviderDialog(viewController)`](#presentTvDialog)

      * Triggered by [getAuthentication()](#getAuthN) when the current requestor supports at least on MVPD that has SSO support.
      * The viewController parameter is the Apple SSO Dialog and needs to be presented on the main view controller.

    * [`dismissTvProviderDialog(viewController)`](#dismissTvDialog)

      * Triggered by a user action (by selecting "Cancel" or "Other TV Providers" from the Apple SSO Dialog).
      * The viewController parameter is the Apple SSO Dialog and needs to be dismissed from the main view controller.

![](../../../../assets/iOS-flows.png)

### B. Startup Flow {#startup_flow}

1.  Start the upper-level application.</br>
1.  Initiate Adobe Pass Authentication </br>

    a.  Call [`init`](#$init) to create a single instance of the Adobe Pass Authentication AccessEnabler.
    * **Dependency:** Adobe Pass Authentication Native iOS/tvOS Library (AccessEnabler)
    
    b.  Call `setRequestor()` to establish the identity of the Programmer; pass in the Programmer's `requestorID` and(optionally) an array of Adobe Pass Authentication endpoints. For tvOS you will also need to provide the public key and the secret. See [Clientless documentation](#create_dev) for details.

    *   **Dependency:** Valid Adobe Pass Authentication RequestorID (Work with your Adobe Pass Authentication Account
      Manager to arrange this).

    *   **Triggers:**
      [setRequestorComplete()](#$setReqComplete) callback.

    >[!NOTE]
    >
    >No entitlement requests can be completed until the requestor identity is fully established. This effectively means that while [`setRequestor()`](#$setReq)  is still running, all subsequent entitlement requests. For example, [`checkAuthentication()`](#checkAuthN) are blocked.

    You have two implementation options: Once the requestor identification information is sent to the backend server, the UI application layer may choose one of the two following approaches: </br>

    1.  Wait for the triggering of the [`setRequestorComplete()`](#setReqComplete) callback (part of the AccessEnabler delegate). This option provides the most certainty that [`setRequestor()`](#$setReq) completed, so it is recommended for most implementations.

    1.  Continue without waiting for the triggering of the [`setRequestorComplete()`](#setReqComplete) callback, and start issuing entitlement requests. These calls (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) are queued by the AccessEnabler library, which will make the actual network calls after the [`setRequestor()`](#$setReq). This option can occasionally be disrupted if, for example, the network connection is unstable.

1.  Call `checkAuthentication()` to check for an existing authentication without initiating the full Authentication flow.  If this call succeeds, you can proceed directly to the Authorization flow. If not, proceed to the Authentication flow.

    *   **Dependency:** A successful call to [setRequestor()](#$setReq) (this dependency applies to all subsequent calls as well).

    *   **Triggers:** [setAuthenticationStatus()](#$setAuthNStatus) callback.


### C. Authentication Flow without Apple SSO {#authn_flow_wo_applesso}

1.  Call [`getAuthentication()`](#$getAuthN) to initiate the authentication flow, or to get confirmation that the user is already
    authenticated.

    **Triggers:**

    *   The [setAuthenticationStatus()](#$setAuthNStatus) callback, if the user is already authenticated. In this case, proceed directly to the [Authorization Flow](#authz_flow).

    *   The [displayProviderDialog()](#$dispProvDialog) callback, if the user is not yet authenticated.

1.  Present the user with the list of providers sent to
    [`displayProviderDialog()`](#dispProvDialog).

1.  After the user selects a provider, obtain the URL of the user's MVPD from the `navigateToUrl:` or `navigateToUrl:useSVC:` callback and open a `UIWebView/WKWebView` or `SFSafariViewController` controller and direct that controller to the URL.

1.  Through the `UIWebView/WKWebView` or `SFSafariViewController` instantiated in the previous step, the user lands on the MVPD's login page and inputs login credentials. Several redirect operations take place within the controller.</br>

>[!NOTE]
>
>At this point, the user has the opportunity to cancel the authentication flow. If this occurs, your UI layer is responsible for informing the AccessEnabler about this event by calling [setSelectedProvider()](#setSelProv) with `null` as a parameter. This allows the AccessEnabler to clean up it's internal state and reset the Authentication Flow.

1.  Upon a successful login by the user, your application layer detects the loading of a specific custom URL. Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the authentication flow has completed and that it is safe to close the `UIWebView/WKWebView` or `SFSafariViewController` controller. In case a `SFSafariViewController`controller is required to be used the specifc custom URL is defined by the **`application's custom scheme`** (e.g.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the **`ADOBEPASS_REDIRECT_URL`** constant (that is, `adobepass://ios.app`).

1.  Close the UIWebView/WKWebView or SFSafariViewController controller and call AccessEnabler's `handleExternalURL:url` API method, which instructs the AccessEnabler to retrieve the authentication token from the backend server.

1.  (Optional) Call [`checkPreauthorizedResources(resources)`](#$checkPreauth) to check which resources the user is authorized to view. The `resources` parameter is an array of protected resources that is associated with the user's authentication token. One use for the authorization information obtained from the user's MVPD is to decorate your UI(for example, locked / unlocked symbols next to protected content).

    * **Triggers:** [`preauthorizedResources()`](#preauthResources) callback  
    * **Execution point:** After the completed Authentication Flow

1.  If authentication was successful, proceed to the Authorization Flow.

### D. Authentication Flow with Apple SSO on iOS {#authn_flow_with_applesso}

1.  Call [`getAuthentication()`](#$getAuthN) to initiate the authentication flow, or to get confirmation that the user is already authenticated.
    **Triggers:**

    * The [presentTvProviderDialog()](#presentTvDialog) callback, if the user is not authenticated and the current requestor has at least on MVPD that supports SSO. If no MVPDs support SSO, the classic authentication flow will be used.

1.  After the user selects a provider the AccessEnabler library will obtain an authentication token with the information provided by Apple's VSA framework.

1.  The [setAuthenticatiosStatus()](#setAuthNStatus) callback will be triggered. At this point the user should be authenticated with Apple SSO.

1.  [Optional] Call [`checkPreauthorizedResources(resources)`](#$checkPreauth) to check which resources the user is authorized to view. The `resources` parameter is an array of protected resources that is associated with the user's authentication token. One use for the authorization information obtained from the user's MVPD is to decorate your UI (for example, locked / unlocked symbols next to protected content).

    * **Triggers:** [`preauthorizedResources()`](#preauthResources) callback  
    * **Execution point:** After the completed Authentication Flow

1.  If authentication was successful, proceed to the Authorization Flow.

### E. Authentication Flow with Apple SSO on tvOS {#authn_flow_with_applesso_tvOS}

1.  Call [`getAuthentication()`](#$getAuthN) to initiate the
    authentication flow, or to get confirmation that the user is already
    authenticated.
    **Triggers:**
    * The [`presentTvProviderDialog()`](#presentTvDialog) callback, if the user is not authenticated and the current requestor has at least on MVPD that supports SSO. If no MVPDs support SSO, the classic authentication flow will be used.

1.  After the user selects a provider the [`status()`](#status_callback_implementation) callback will be called. A registration code will be provided and the AccessEnabler library will start polling the server for a successfull second screen authentication.

1.  If the registration code provided was used to successfully authenticate on the second screen, the [`setAuthenticatiosStatus()`](#setAuthNStatus) callback will be triggered. At this point the user should be authenticated with Apple SSO.
1.  [Optional] Call [`checkPreauthorizedResources(resources)`](#$checkPreauth) to check which resources the user is authorized to view. The `resources` parameter is an array of protected resources that is associated with the user's authentication token. One use for the authorization information obtained from the user's MVPD is to decorate your UI (for example, locked / unlocked symbols next to protected content).

    *   **Triggers:** [`preauthorizedResources()`](#preauthResources) callback

    *   **Execution point:** After the completed Authentication Flow
1.  If authentication was successful, proceed to the Authorization Flow.

### F. Authorization Flow {#authz_flow}

1.  Call [getAuthorization()](#$getAuthZ) to initiate the authorization flow.

    * **Dependency:** Valid ResourceID(s) agreed upon with the MVPD(s).
    * Resource IDs should be the same as those used on any other devices or platforms, and will be the same across MVPDs. For information on Resource IDs, see [Identifying Protected Resources](/help/authentication/integration-guide-programmers/features-standard/entitlements/identify-protected-resources.md)

1.  Validate authentication and authorization.

    * If the [getAuthorization()](#$getAuthZ) call succeeds: The user has valid AuthN and AuthZ tokens (the user is authenticated and authorized to watch the requested media).

    * If [getAuthorization()](#$getAuthZ) fails: Examine the exception thrown to determine its type (AuthN, AuthZ, or something else):
      * If it was an authentication (AuthN) error then re-start the authentication flow.
      * If it was an authorization (AuthZ) error then the user is not authorized to watch the requested media and some kind of error message should be displayed to the user.
      * If there was some other type of error (connection error, network error, etc.) then display an appropriate error message to the user.

1.  Validate the Short Media Token.  
    Use the Adobe Pass Authentication Media Token Verifier library to verify the short-lived media token returned from the [getAuthorization()](#$getAuthZ) call above:

    * If the validation succeeds: Play the requested media for the user.
    * If the validation fails: The AuthZ token was invalid, the media request should be refused, and an error message should be displayed to the user.


1.  Return to your normal application flow.

### G. View Media Flow {#media_flow}

1.  User selects the media to view.
1.  Is the media protected? Your application checks if the selected media is protected:
    
    *   If the selected media is protected, your application starts the [Authorization Flow](#authz_flow) above.
  
    *   If the selected media is not protected, then play the media for
        the user.

### H. Logout Flow without Apple SSO {#logout_flow_wo_AppleSSO}

1.  Call [`logout()`](#$logout) to log the user out. The AccessEnabler clears out all cached values and tokens. After clearing out the cache, the AccessEnabler makes a server call to clean the server-side sessions. Note that since the server call could result in a SAML redirect to the IdP (this allows for the session clean-up on the IdP side), this call must follow all redirects. For this reason, this call must be handled inside a UIWebView/WKWebView or SFSafariViewController controller.

    a.  Following the same pattern as the authentication workflow, the AccessEnabler domain makes a request to the UI application layer, via the `navigateToUrl:` or `navigateToUrl:useSVC:` callback, to create a UIWebView/WKWebView or SFSafariViewController controller and instruct that to load the URL provided in the callback's `url` parameter. This is the URL of the logout endpoint on the backend server.
    
    b.  Your application must monitor the activity of the `UIWebView/WKWebView or SFSafariViewController` controller and detect the moment when it loads a specific custom URL, as it goes through several redirects. Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the logout flow has completed and that it is safe to close the `UIWebView/WKWebView` or `SFSafariViewController` controller. When the controller loads this specific custom URL your application must close the `UIWebView/WKWebView or SFSafariViewController` controller and call AccessEnabler's `handleExternalURL:url`API method. In case a `SFSafariViewController`controller is required to be used the specifc custom URL is defined by the **`application's custom scheme`** (for example, `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the **`ADOBEPASS_REDIRECT_URL`**  constant (that is, `adobepass://ios.app`).

      >[!NOTE]
      >
      >The logout flow differs from the authentication flow in that the user is not required to interact with the UIWebView/WKWebView or SFSafariViewController in any way. The UI application layer uses a UIWebView/WKWebView or  SFSafariViewController to make sure that all the redirects are being followed. Therefore, it is possible (and recommended) to make the controller invisible (i.e. hidden) during the logout process.


### I. Logout Flow with Apple SSO {#logout_flow_with_AppleSSO}

1. Call [`logout()`](#$logout) to log the user out.
1. The [status()](#status_callback_implementation) callback will be called with id VSA203.
1. The user should be instructed to login from the system settings also. Failure do so will result in a re-authentication when the application is re-launched.



<!--
### Related Information {#related}


- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Pass
  authentication native SDK (Tech Note)](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->
