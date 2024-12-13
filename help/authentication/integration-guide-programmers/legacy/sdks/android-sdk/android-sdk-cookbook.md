---
title: Android SDK Cookbook
description: Android SDK Cookbook
exl-id: 7f66ab92-f52c-4dae-8016-c93464dd5254
---
# (Legacy) Android SDK Cookbook {#android-sdk-cookbook}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#intro}

This document describes the entitlement workflows that a Programmer's upper-level application can implement through the APIs exposed by the Android AccessEnabler library.


The Adobe Pass Authentication entitlement solution for Android is ultimately divided into two domains:

- The UI domain - this is the upper-level application layer which implements the UI and uses the services provided by the AccessEnabler library to provide access to restricted content.
- The AccessEnabler domain - this is where the entitlement workflows are implemented in the form of:
    - Network calls made to Adobe's backend servers
    - Business-logic rules related to the authentication and authorization workflows
    - Management of various resources and processing of workflow state (such as the token cache)

The goal of the AccessEnabler domain is to hide all the complexities of the entitlement workflows, and provide to the upper-layer application (through the AccessEnabler library) a set of simple entitlement primitives with which you implement the entitlement workflows:

1.  Set the requestor identity.

1.  Check and get authentication against a particular identity provider.

1.  Check and get authorization for a particular resource.

1.  Logout.

The AccessEnabler's network activity takes place in a different thread so the UI thread is never blocked. As a result, the two-way communication channel between the two application domains must follow a fully asynchronous pattern:

- The UI application layer sends messages to the AccessEnabler domain via the API calls exposed by the AccessEnabler library.
- The AccessEnabler responds to the UI layer through the callback methods included in the AccessEnabler protocol which the UI layer registers with the AccessEnabler library.

## Entitlement Flows {#entitlement}

1.  [Prerequisites](#prereqs)
1.  [Startup Flow](#startup_flow)
1.  [Authentication Flow](#authn_flow)
1.  [Authorization Flow](#authz_flow)
1.  [View Media Flow](#media_flow)
1.  [Logout Flow](#logout_flow)

### A. Prerequisites {#prereqs}

1.  Create your callback functions:
      - [`setRequestorComplete()`](#$setRequestorComplete)

          Triggered by `setRequestor()`, returns success or failure.    
          Success indicates you can proceed with entitlement calls.

      - [displayProviderDialog(mvpds)](#$displayProviderDialog)

          Triggered by `getAuthentication()` only if the user has not selected a provider (MVPD) and is not yet authenticated.     
          The `mvpds` parameter is an array of providers available to the user.

      - [`setAuthenticationStatus(status, errorcode)`](#$setAuthNStatus)

          Triggered by `checkAuthentication()` every time.  
          Triggered by `getAuthentication()` only if the user is already authenticated and has selected a provider.

          Status returned is success or failure, the errorcode describes the type of the failure.

      - [navigateToUrl(url)](#$navigateToUrl)

          Triggered by `getAuthentication()` after the user selects an MVPD. The `url` parameter provides the location of the MVPD's login page.

      - [`sendTrackingData(event, data)`](#$sendTrackingData)

          Triggered by `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.  
          The `event` parameter indicates which entitlement event occurred; the `data` parameter is a list of values relating to the event. 

      - [`setToken(token, resource)`](#$setToken)

          Triggered by `checkAuthorization()` and `getAuthorization()` after a successful authorization to view a resource.  
          The `token` parameter is the short-lived media token; the `resource` parameter is the content that the user is authorized to view.

      - [`tokenRequestFailed(resource, code, description)`](#$tokenRequestFailed)

          Triggered by `checkAuthorization()` and `getAuthorization()` after an unsuccessful authorization.  
          The `resource` parameter is the content that the user was attempting to view; the `code` parameter is the error code indicating what type of failure occurred; the `description` parameter describes the error associated with the error code.

      - [`selectedProvider(mvpd)`](#$selectedProvider)

          Triggered by `getSelectedProvider()`.  
          The `mvpd` parameter provides information about the provider selected by the user.

      - [`setMetadataStatus(metadata, key, arguments)`](#$setMetadataStatus)

          Triggered by `getMetadata().`  
          The `metadata` parameter provides the specific data you requested; the `key` parameter is the key used in the `getMetadata()` request; and the `arguments` parameter is the same dictionary that was passed to `getMetadata()`.

      - [`preauthorizedResources(resources)`](#$preauthResources)

          Triggered by `checkPreauthorizedResources()`.  
          The `authorizedResources` parameter presents the resources that the user is authorized to view.  
 

![](../../../../assets/android-entitlement-flows.png)  
 

### B. Startup Flow {#startup_flow}

1.  Start the upper-level application.
1.  Initiate Adobe Pass Authentication

    a.  Call [`getInstance`](#$getInstance) to create a single instance of the Adobe Pass Authentication AccessEnabler.
        
      - **Dependency:** Adobe Pass Authentication Native
        Android Library (AccessEnabler)
    
    b.  Call` setRequestor()` to establish the identify of the Programmer; pass in the Programmer's `requestorID` and (optionally) an array of Adobe Pass Authentication endpoints.
        
      - **Dependency:** Valid Adobe Pass Authentication RequestorID  
        (Work with your Adobe Pass Authentication Account Manager to arrange this.)
    
      - **Triggers:** setRequestorComplete() callback

    |NOTE|     |
    | --- | --- |  
    | ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/icons/1313859077_lightbulb.png) | No entitlement requests can be completed until the requestor identity is fully established. This effectively means that while setRequestor() is still running, all subsequent entitlement requests (for example, `checkAuthentication()`) are blocked.<br><br>You have two implementation options: Once the requestor identification information is sent to the backend server, the UI application layer may choose one of the two following approaches:<br><br>1.  Wait for the triggering of the `setRequestorComplete()` callback (part of the AccessEnabler delegate).  This option provides the most certainty that `setRequestor()` completed, so it is recommended for most implementations.<br>2.  Continue without waiting for the triggering of the `setRequestorComplete()` callback, and start issuing entitlement requests. These calls (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) are queued by the AccessEnabler library, which will make the actual network calls after the `setRequestor(). `This option can occasionally be disrupted if for example, the network connection is unstable. |

1.  Call [checkAuthentication()](#$checkAuthN) to check for an existing authentication without initiating the full Authentication flow.   If this call succeeds, you can proceed directly to the Authorization flow.  If not, proceed to the Authentication flow.

    - **Dependency:** A successful call to `setRequestor()` (this dependency applies to all subsequent calls as well).

    - **Triggers:** setAuthenticationStatus() callback

### C. Authentication Flow {#authn_flow}

1.  Call [`getAuthentication()`](#$getAuthN) to initiate the authentication flow, or to get confirmation that the user is already authenticated.   
    **Triggers:**  
    - The setAuthenticationStatus() callback, if the user is already authenticated.  In this case, proceed directly to the [Authorization Flow](#authz_flow).
    - The displayProviderDialog() callback, if the user is not yet authenticated.  

1.  Present the user with the list of providers sent to `displayProviderDialog()`.

1.  After the user selects a provider, obtain the URL of the user's MVPD from the `navigateToUrl()` callback.  Open a WebView and direct that WebView control to the URL.   

1.  Through the WebView instantiated in the previous step, the user lands on the MVPD's login page and inputs login credentials. Several redirect operations take place within the WebView.  
     
    **Note:** At this point, the user has the opportunity to cancel the authentication flow. If this occurs, your UI layer is responsible for informing the AccessEnabler about this event by calling `setSelectedProvider()` with `null` as a parameter. This allows the AccessEnabler to clean up it's internal state and reset the Authentication Flow.

1.  Upon a succesful login by the user, your application layer detects the loading of a "custom redirect URL" (i.e.: `http://adobepass.android.app`). This custom URL is actually an invalid URL that is not intended for the WebView to load. It is a signal that the Authentication Flow has completed, and that the WebView needs to be closed.

1.  Close the WebView control and call `getAuthenticationToken()`, which instructs the AccessEnabler to retrieve the authentication token from the backend server. 

1.  [Optional] Call [`checkPreauthorizedResources(resources)`](#$checkPreauth) to check which resources the user is authorized to view. The `resources` parameter is an array of protected resources that is associated with the user's authentication token.  
    **Triggers:** `preAuthorizedResources()` callback  
    **Execution point:** After the completed Authentication Flow

1.  If authentication was successful, proceed to the Authorization Flow.

 

### D. Authorization Flow {#authz_flow}

1.  Call [getAuthorization()](#$getAuthZ) to initiate the authorization
    flow.

    Dependency: Valid ResourceID(s) agreed upon with the MVPD(s).

    **Note:** ResourceIDs should be the same as those used on any other devices or platforms, and will be the same across MVPDs.

1.  Validate authentication and authorization.

    - If the `getAuthorization()` call succeeds: The user has valid AuthN and AuthZ tokens (the user is authenticated and authorized to watch the requested media).
    - If `getAuthorization()` fails: Examine the exception thrown to determine its type (AuthN, AuthZ, or something else):
        - If it was an authentication (AuthN) error then re-start the authentication flow.
        - If it was an authorization (AuthZ) error then the user is not authorized to watch the requested media and some kind of error message should be displayed to the user.
        - If there was some other type of error (connection error, network error, etc.) then display an appropriate error message to the user.

1.  Validate the Short Media Token.  
    Use the Adobe Pass Authentication Media Token Verifier library to to verify the short-lived media token returned from the `getAuthorization()` call above:

    - If the validation succeeds: Play the requested media for the user.
    - If the validation fails: The AuthZ token was invalid, the media request should be refused, and an error message should be displayed to the user.

1.  Return to your normal application flow.

### E. View Media Flow {#media_flow}

1.  User selects the media to view.
2.   Is the media protected?  Your application checks if the selected media is protected:
    - If the selected media is protected, your application starts the [Authorization Flow](#authz_flow) above.
    - If the selected media is not protected, then play the media for the user.

 

### F. Logout Flow {#logout_flow}

1.  Call [`logout()`](#$logout) to log the user out.   
    The AccessEnabler clears out all cached values and tokens for the current MVPD for current requestor and also for requestors with Single Sign On. After clearing out the cache, the AccessEnabler makes a server call to clean the server-side sessions.  Note that since the server call could result in a SAML redirect to the IdP (this allows for the session clean-up on the IdP side), this call must follow all redirects. For this reason, this call must be handled inside a WebView control.

    a.  Following the same pattern as the authentication workflow, the AccessEnabler domain makes a request to the UI application layer (via the`navigateToUrl()` callback) to create a WebView control and instruct that control to load the URL of the logout endpoint on the backend server.
    
    b.  Again, the UI must monitor the activity of the WebView control and detect the moment when the control, as it goes through several redirects, loads the application's custom URL (i.e.: `http://adobepass.android.app/`). Once this event takes place, the UI application layer closes the WebView and the logout process is complete.

    **Note:** The logout flow differs from the authentication flow in that the user is not required to interact with the WebView in any way. The UI application layer uses a WebView to make sure that all the redirects are being followed. Thus it is possible (and recommended) to make the WebView control invisible (i.e. hidden) during the logout process.

 

### User Flows for Login with mutiple MVPDs and Logout {#user_flows}

[Here](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AndroidSSOUserFlows.pdf) you have a document describing the behavior when using multiple MVPDs and what's happening when the user logs out from an application.

The described behavior is available when using Android SDK version >= 2.0.0.
