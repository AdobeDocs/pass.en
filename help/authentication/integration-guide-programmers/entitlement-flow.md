---
title: The programmer entitlement flow
description: The programmer entitlement flow
exl-id: b1c8623a-55da-4b7b-9827-73a9fe90ebac
---
# The programmer entitlement flow {#prog-entitlement-flow}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

This document describes the basic entitlement flow from the Programmer's perspective.  For information on features and use cases beyond the basic TVE integration covered here, see [Programmer use cases](/help/authentication/integration-guide-programmers/programmer-use-cases.md).   

Adobe Pass Authentication mediates the entitlement flow between Programmers and MVPDs by providing secure, consistent interfaces for both parties.  On the Programmer's side, Adobe Pass Authentication provides two general types of entitlement interface:

1. AccessEnabler - A client component that provides a library of APIs for apps on devices that can render web pages (e.g., web apps, smartphone / tablet apps).  
2. Clientless API - RESTful web services for devices that cannot render web pages (e.g., set-top boxes, game consoles, smart TVs). The requirement for rendering web pages comes from the MVPD's requirement that users authenticate on the MVPD's website.

In addition to the platform-neutral overview presented here, there is a Clientless API-specific overview here: Clientless API documentation. The AccessEnabler runs natively on supported platforms (AS / JS on Web, Objective-C on iOS, and Java on Android). The AccessEnabler APIs are consistent across the supported platforms. All of the platforms that do not support AccessEnabler use the same Clientless API.

For both types of interface, Adobe Pass Authentication securely mediates the entitlement flow between the Programmer's app and the user's MVPD:

![](../assets/prog-entitlement-flow.png)


*Figure: Adobe Pass Authentication Ecosystem*

>[!IMPORTANT]
>
>Note in the diagram above that there is one part of the entitlement flow that does not go through Adobe Pass Authentication servers: the MVPD login. Users must log on to their MVPD's login page. Because of this requirement, on devices that cannot render web pages, the Programmer's app must direct users to switch to a web-capable device to log in with their MVPD, after which they return to the original device for the remainder of the entitlement flow.

## Entitlement Flow {#entitlement-flow}

There are four distinct sub-flows that make up the basic entitlement
flow:

1. [Startup Flow](/help/authentication/integration-guide-programmers/entitlement-flow.md#startup)
1. [Authentication Flow](/help/authentication/integration-guide-programmers/entitlement-flow.md#authentication)
1. [Authorization Flow](/help/authentication/integration-guide-programmers/entitlement-flow.md#authorization)
1. [Logout FLow](/help/authentication/integration-guide-programmers/entitlement-flow.md#logout)

On a user's initial visit to a Programmer's site the entitlement flow proceeds in the order above. However, on subsequent visits, depending upon whether authentication and authorization tokens have expired or not, or depending upon viewing policies, a user might only go through one or two of the sub-flows.

### Startup Flow {#startup}

Establishes the identity of the Programmer and the device, performs initialization tasks. This is a prerequisite for all subsequent entitlement calls.

**AccessEnabler**

*   **`setRequestor()`** - Establishes your identify with the AccessEnalber, and by extension, the Adobe Pass Authentication servers. This call is a precursor to the rest of the entitlement flow. For example, in JavaScript:

    ```JavaScript
      /* Define the requestor ID (Programmer/aggregator ID). */
        var requestorID = "sample_requestor_Id";
        ...
        // Callback indicating that the AccessEnabler swf has initialized
        function swfLoaded() {
            // AccessEnabler is loaded so we can use the API function it provides
            accessEnablerObject.setRequestor(requestorID); 
        ...
        }

    ```

**Clientless API**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`** - Depending upon the platform, there may be prerequisite tasks to complete before your app calls regcode. See the **Clientless API documentation** for details. For example, the Xbox platforms require you to complete prescribed security steps prior to calling regcode.

### Authentication Flow {#authentication}

Successful authentication generates an AuthN token tied to the device and requestor. Successful authentication is a prerequisite for Authorization.

**AccessEnabler**

* `checkAuthentication()` - Checks if a valid cached authentication token exists in the local token cache, without actually triggering the full authentication flow. This triggers the `setAuthenticationStatus()` callback function.
* `getAuthentication()` - Initiates the full authentication flow. If successful, Adobe Pass Authentication generates an AuthN token, and caches it on the client. The user logs in on their selected MVPDs site, presented either in an iFrame, Popup window, or a webview, depending upon the platform. This triggers the displayProviderDialog().

**Clientless API**

* `<FQDN>/.../checkauthn` - The web service version of `checkAuthentication()` above.
* `<FQDN>/.../config` - Returns the list of MVPDs to the 2nd-screen app.
* `<FQDN>/.../authenticate` - Initiates the authentication flow from the 2nd-screen app, redirecting users to their selected MVPD for login. If successful, Adobe Pass Authentication generates an AuthN token and stores it on the server, and the user returns to their original device to complete the entitlement flow.

An AuthN token is considered valid if the following two points are true:

* The AuthN token is not expired
* The MVPD associated with the AuthN token is on the list of allowed MVPDs for the current Requestor ID

#### Generic AccessEnabler Initial Authentication Workflow {#generic-ae-initial-authn-flow}

1.  Your app initiates the authentication workflow with a call to `getAuthentication()`, which checks for a valid cached authentication token. This method has an optional `redirectURL` parameter; if you do not supply a value for `redirectURL`, after a successful authentication the user is returned to the URL from which the authentication was initialized.
1.  The AccessEnabler determines the current authentication status. If the user is currently authenticated, the AccessEnabler calls your `setAuthenticationStatus()` callback function, passing an authentication status indicating success.
1.  If the user is not authenticated, the AccessEnabler continues the authentication flow by determining whether the user's last authentication attempt was successful with a given MVPD. If an MVPD ID is cached AND the `canAuthenticate` flag is true OR an MVPD was selected using `setSelectedProvider()`, the user is not prompted with the MVPD selection dialog. The authentication flow continues using the cached value of the MVPD (that is, the same MVPD that was used during the last successful authentication). A network call is made to the backend server, and the user is redirected to the MVPD login page.

1.  If no MVPD ID is cached AND no MVPD was selected using `setSelectedProvider()` OR the `canAuthenticate` flag is set to false, the `displayProviderDialog()` callback is called. This callback directs your app to create the UI that presents the user a list of MVPDs to choose from. An array of MVPD objects is provided, containing the necessary information for you to build the MVPD selector. Each MVPD object describes an MVPD entity, and contains information such as the ID of the MVPD and the URL where the MVPD logo can be found.

1.  Once an MVPD is selected, your app must inform the AccessEnabler of the user's choice. For non-Flash clients, once the user selects the desired MVPD, you inform the AccessEnabler of the user selection via a call to the `setSelectedProvider()` method. Flash clients instead dispatch a shared `MVPDEvent` of type "`mvpdSelection`", passing the selected provider.

1.  When the AccessEnabler is informed of the user's MVPD selection, a network call is made to the backend server, and the user is redirected to the MVPD login page.

1.  Within the authentication workflow, the AccessEnabler communicates with Adobe Pass Authentication and the selected MVPD to solicit the user's credentials (user ID and password) and to verify their identity. While some MVPDs redirect to their own site for the login, others require you to display their login page within an iFrame. Your page must include the callback that creates an iFrame, in case the customer chooses one of those MVPDs.<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->.

1.  Once the user has successfully logged in, the AccessEnabler retrieves the authentication token and informs your app that the authentication flow is complete. The AccessEnabler calls the `setAuthenticationStatus()` callback with a status code of 1, indicating success. If there is an error during the execution of these steps, the `setAuthenticationStatus()` callback is triggered with a status code of 0, indicating authentication failure, as well as a corresponding error code.

>[!IMPORTANT]
>Comcast is the only MVPD at the moment that doesn't provide a static URL for the logo. Programmers should pull the latest up-to-date logos from [XFINITY Developer's portal](https://developers.xfinity.com/products/tv-everywhere).
>

### Authorization Flow {#authorization}

Authorization is a prerequisite for viewing protected content. Successful authorization generates an AuthZ token, along with a short-lived Media Token that is provided to the Programmer's app for security purposes. Note that, to support the authorization workflow, you must have previously performed the necessary requestor setup and have integrated the [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-token-verifier-int.md). With these completed, you can initiate authorization.

Your app initiates authorization when a user requests access to a protected resource. You pass a resource ID specifying the requested resource (for example , a channel, episode, etc.). Your app first checks for a stored authentication token. If one is not found, you initiate the authentication process.

**AccessEnabler**

*   `checkAuthorization()` - Checks authorization without initiating the full authorization flow. This is often used to update status information displayed in the Programmer app's UI.

*   `getAuthorization()` - Initiates the full authorization flow.

You provide the following callback functions to handle the results of
the authorization call:

*   `setToken()` - If authentication was previously successful and authorization succeeds, the AccessEnabler calls your `setToken()` callback function, passing the short-lived media token, indicating a successful conclusion to the Adobe Pass Authentication entitlement flow. (Before allowing the user to view protected content, the Programmer's app checks the validity of the Media Token using the Media Token Verifier.

*   `tokenRequestFailed()` - If the user is not authorized for the requested resource (or if the query fails for any other reason), the AccessEnabler calls this callback function (plus your own error reporting functions), passing details on the failure.

**Clientless API**

* `\<FQDN\>/.../authorize` - Initiates the full authorization flow.

#### Generic AccessEnabler Authorization Workflow {#generic-ae-authr-wf}

1.  Provide a callback function that registers your assigned programmer GUID with the Access Enabler, using `setReqestor()`. This callback function is called when the AccessEnabler has been
    downloaded successfully.

1.  Call `getAuthorization()` when a user requests access to a protected resource. Using `getAuthorization()`, pass a resource ID specifying the requested resource (for example , a channel, episode, etc.). The AccessEnabler looks for a cached authentication token to pass with the authorization request. If one is not found, it initiates the authentication flow.
1.  Provide callback functions to handle the results of authorization:

      *   `setToken()` - If authorization succeeds or if the user has previously been authorized, the Access Enabler continues with the authorization process by calling your `setToken()` callback function, passing the short-lived authorization token.

      *   `tokenRequestFailed()` - If the user is not authorized for the requested resource (or if the query fails for any other reason), the AccessEnabler calls any error reporting functions you have registered, plus the `tokenRequestFailed()` callback, passing details on the failure.

### Logout flow {#logout}

Clears tokens and other data associated with the current user's entitlement flow.

**AccessEnabler**

* `logout()`

**Clientless API**

* `\<FQDN\>/.../logout`

## Understand AccessEnabler behavior {#ae-behavior}

All AccessEnabler API calls are asynchronous (with one exception, noted in the API references). You can call an API an arbitrary number of times, however there is no strong guarantee that the actions triggered
by the calls will be completed in the same order that the calls were made. (An exception to this is the current Flash Player runtime; not being multi-threaded it will ensure calls *do* complete in the order
they are called.)

In order to distinguish between responses, and be able to pair responses with calls, all callbacks echo back their input parameters. This includes `setToken()` and`tokenRequestFailed()`, which are triggered ultimately by `checkAuthorization()`. (For `checkAuthorization()` callbacks, the resource used is echoed back.) Taking advantage of this feature, you can distinguish which response corresponds to which call. To use this feature you could code something like the following:

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }

```

### AE Behavior FAQ {#ae-beh-faq}

**Question. What happens if I make a second AccessEnabler call before the first call finishes?**

The first call continues to execute as the second call executes (asynchronous communications).  

**Question. Is there a maximum number of simultaneous calls that AccessEnabler can support?**

No limit is set explicitly in the AccessEnabler code, so you are limited only by your available system resources, as well as by the MVPD's capacity.

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->
