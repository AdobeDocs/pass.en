---
title: Refresh-less Login and Logout
description: Refresh-less Login and Logout
exl-id: 3ce8dfec-279a-4d10-93b4-1fbb18276543
---
# (Legacy) Refresh-less Login and Logout {#tefresh-less-login-and-logout}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

For web applications, you must account for some different possible scenarios for authenticating and logging out users.  MVPDs require that users log in on the MVPD's web page to authenticate, with the following additional factors coming into play:

- Some MVPDs require a full redirect from your site to their login page
- Some MVPDs require you to open an iFrame on your site to display the MVPD's login page
- Some browsers do not handle the iFrame scenario well, so for those browsers a better alternative is to use a popup window instead of the iFrame

Prior to Adobe Pass Authentication 2.7, all of these scenarios for authenticating a user involved a full page refresh of the Programmer's page.For 2.7 and subsequent releases, the Adobe Pass Authentication team improved these flows so that the user does not have to experience a page refresh on your app during login and logout.  


## Detailed Description {#detailed_description}

Let's begin with a summary of the original authentication and logout flows, then follow that with the improved authentication and logout flows. Note that the first four sections address normal MVPDs (non-TempPass), while the last section describes the special implementation that needs to be applied for TempPass:

- [Original Authentication Flow](#orig_authn)
- [Original Logout Flow](#orig_logout)
- [Improved Authentication Flow](#improved_authn)
- [Improved Logout Flow](#improved_logout)
- [TempPass Flow](#improved_temppass)

</br>

## Original Authentication / Logout Flows {#orig_authn}

**Authentication**

The Adobe Pass Authentication web clients have two ways of authenticating, depending upon the requirements of MVPDs:

1.  **Full-page Redirect -** After the user selects a provider    (configured with full-page redirect) from the MVPD picker on the    Programmer's website, `setSelectedProvider(<mvpd>)` is invoked on the AccessEnabler and the user is redirected to the MVPD's login page. After the user provides valid credentials he is redirected back to the Programmer's website. The AccessEnabler is initialized and the authentication token is retrieved from Adobe Pass Authentication during `setRequestor`.
1.  **iFrame / Popup Window -** After the user selects a provider (configured with iFrame), `setSelectedProvider(<mvpd>)` is invoked on the AccessEnabler. This action will trigger the `createIFrame(width, height)` callback, notifying the Programmer to create an iFrame (or popup - depending on the browser/preferences) with the name `"mvpdframe"` and the provided dimensions. After the iFrame/popup is created, the AccessEnabler loads the MVPD's login page in the iFrame/popup. The user provides valid credentials and the iFrame/popup is redirected to Adobe Pass Authentication, which returns a JS snippet that closes the iFrame/popup and reloads the parent page (Programmer website). Similarly to flow 1, the authentication token is retrieved during `setRequestor`. 

The `displayProviderDialog` callback (triggered by `getAuthentication`/`getAuthorization`) returns a list of MVPDs and their appropriate settings. The `iFrameRequired` property of an MVPD allows the Programmer to know if it should activate flow 1 or flow 2. Note that the Programmer is required to take extra action (creating an iFrame/popup) only for flow 2.

**Cancel Authentication**

There is also the situation in which the user explicitly cancels the authentication flow by closing the login page. Here are the scenarios and the proposed solution to the Programmers:

1.  **Full-page redirect -** When the login page is closed, the  user will need to navigate to the Programmer's website again and initiate the entire flow from the beginning. No explicit action is required on the Programmer's side in this scenario.
1.  **iFrame -** The Programmer is recommended to host the iFrame inside a `div` (or similar UI component) that has a Close button attached to it. When the user presses the Close button, the Programmer will destroy the iFrame along with the associated UI and perform `setSelectedProvider(null)`. This call allows the AccessEnabler to clear its internal state and makes it possible for the user to initiate a subsequent authentication flow. `setAuthenticationStatus` and `sendTrackingData(AUTHENTICATION_DETECTION...)` will be triggered to signal a failed authentication flow (both on `getAuthentication` and `getAuthorization`).
1.  **Popup -** Some browsers cannot accurately detect the window close event, so a different approach needs to be taken here (in contrast to the iFrame flow above). Adobe recommends that the Programmer initializes a timer that periodically verifies the existence of the login popup. If the window does not exist, the Programmer can be sure that the user manually cancelled the login flow, and the Programmer can proceed with calling `setSelectedProvider(null)`. The triggered callbacks are the same as in flow 2 above. 

</br>

## Original Logout Flow {#orig_logout}

The logout API of the AccessEnabler clears the local state of the library and loads the MVPD's logout URL inthe current tab/window. The browser navigates to the MVPD's logout endpoint and after the process is complete, the user is redirected back to the Programmer's website. The only action that is required on the user's behalf is pressing the Logout button/link and initiating the flow; no user interaction is required on the MVPD's logout endpoint.

**Original Authentication / Logout Flow With Page Refresh**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## Improved (Refresh-less) Authentication {#improved_authn}

>[!NOTE] 
>
>The improved refresh-less login and logout flows require that the browser support modern HTML5 technologies including web messaging.  

Both the authentication (login) and logout flows discussed above provide a similar user experience by reloading the main page after each flow is completed.  The current feature aims to improve the user experience by providing refresh-less (background) login and logout. The Programmer can enable/disable background login and logout by passing two boolean flags (`backgroundLogin` and `backgroundLogout`) to the `configInfo` parameter of the `setRequestor` API. By default, background login/logout are disabled (this provides compatibility with the previous implementation).

**Example:**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**Authentication**

The following points describe the transition between the original authentication flows and the improved flows:

1. The full-page redirect is replaced with a new browser tab in which the MVPD login is performed. The Programmer is required to create a new tab (via `window.open`) named `mvpdwindow` when the user selects an MVPD (with `iFrameRequired = false`). The Programmer then executes `setSelectedProvider(<mvpd>)`, allowing the AccessEnabler to load the MVPD login URL in the new tab. After the user provides valid credentials, Adobe Pass Authentication will close the tab and send a window.postMessage to the Programmer's website that signals to the AccessEnabler that the authentication flow has finished. The following callbacks are triggered:

    - If the flow was initiated by `getAuthentication`: `setAuthenticationStatus` and `sendTrackingData(AUTHENTICATION_DETECTION...)` will be triggered to signal successful/unsuccessful authentication.

    - If the flow was initiated by `getAuthorization`: `setToken/tokenRequestFailed` and `sendTrackingData(AUTHORIZATION_DETECTION...)` will be triggered to signal successful/unsuccessful authorization.

1.  The iFrame / popup window flow remains mostly unchanged, with the difference being that after the user provides valid credentials, the parent page will not be reloaded. The iFrame/popup will automatically close after login and a `window.postMessage` is sent to the parent page, notifying the AccessEnabler that the flow has finished. The same callbacks are triggered as in the previous flow, **plus the following new callback: `destroyIFrame`**. The `destroyIFrame` callback allows the Programmer to remove any iFrame associated/auxiliary components, such as UI decorations. The existence of this callback was not required in the old authentication flow because after the login was complete, Adobe Pass Authentication would reload the Programmer's page, thus destroying all UI components on it.  

</br>     

>[!IMPORTANT] 
> 
>You must load the MVPD login iFrame or popup window as a direct child of the page that contains the AccessEnabler instance. If the MVPD login iFrame or popup window is nested two or more levels down below the page containing the AccessEnabler instance, the flow could hang. For example, if you had an iFrame situated between the main page and the MVPD iFrame (Page =\> iFrame =\> MVPD iFrame), the login flow could fail.

</br>

 **Cancel Authentication**

These are the flows for canceling authentication:

1.  **Browser tab -** Since the tab is basically a new window, capturing its close event has the same limitations as discussed in scenario 3 from the old authentication flows. Moreover, the timer approach is not possible here, because there is no way of distinguishing between a tab that was closed manually by the user and a tab that was closed automatically at the end of the login flow. The solution here is for the AccessEnabler to remain 'silent'(no callbacks are triggered) when the user cancels the flow. Also, the Programmer is not required to take any specific action. The user will be able to initiate another authentication flow without receiving the "Multiple Authentication Requests Error" error (this error has been disabled in the AccessEnabler for background login).

1.  **iFrame -** The Programmer can take the approach discussed in scenario 2 from the old authentication flows (create wrapper UI from the iFrame and associated Close button that triggers `setSelectedProvider(null)`. Although this approach is no longer a strong requirement (multiple authentication flows are allowed for background login, as discussed in scenario 1 above), it is still recommended by Adobe.

1.  **Popup -** This is identical to the Browser tab flow above.

</br>

## Improved Logout Flow {#improved_logout}

The new logout flow will be performed in a hidden iFrame, thus eliminating the full page redirect.  This is possible because the user does not need to take specific action on the MVPD's logout page.

After the logout flow is complete, it will redirect the iFrame to a custom Adobe Pass Authentication endpoint. This will serve a JS snippet that performs a `window.postMessage` to the parent, notifying the AccessEnabler that logout is complete. The following callbacks are triggered: `setAuthenticationStatus()` and `sendTrackingData(AUTHENTICATION_DETECTION ...)`, signaling that the user is no longer authenticated. 

The illustration below shows the refresh-less flow that enables a user to log in to their MVPD without refreshing your application's mainpage:

**Improved (Refresh-less) Authentication / Logout Flow**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass Flow {#improved_temppas}

Refresh-less login follows a different approach for MVPDs of type TempPass.

Since the TempPass flow requires that a window be created automatically, and closed without explicit user interaction, it may pose a problem forsome browsers (popup blockers). Therefore, the AccessEnabler implements the login phase behind the scenes, without requiring a web container created by the Programmer.

Here are the aspects that the Programmer needs to be aware of when implementing TempPass for Refresh-less login and logout:

- Before starting authentication, the iFrame or popup window needs to be created only for non-TempPass MVPDs. The Programmer can detect if an MVPD is TempPass or not by reading the `tempPass` property of the MVPD object (returned by `setConfig()` / `displayProviderDialog()`).

- The `createIFrame()` callback must contain a check for TempPass, and execute its logic only when the MVPD is NOT TempPass.

- The `destroyIFrame()` callback must contain a check for TempPass, and execute its logic only when the MVPD is NOT TempPass.

- The `setAuthenticationStatus()` and `sendTrackingData()` callbacks are invoked after authentication completes (exactly as in the Refresh-less flow for normal MVPDs).

>[!NOTE] 
>
>This flow is available only for Refresh-less TempPass. For the refresh flow, TempPass needs to be handled explicitly (when TempPass requires iFrame / popup)

</br>

The following code sample demonstrates how to handle an MVPD window on a Programmer's website (both for normal MVPDs and for TempPass):

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```
