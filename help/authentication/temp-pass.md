---
title: Temp pass
description: Temp pass
exl-id: 1df14090-8e71-4e3e-82d8-f441d07c6f64
---
# Temp pass {#temp-pass}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Feature summary {#tempass-featur-summary}

Temp Pass lets Programmers offer temporary access to their protected content, for users who don't have account credentials with an MVPD.  Temp Pass includes the following capabilities:

*   Temp Pass can be configured to provide temporary access to cover a variety of scenarios, including the following:
    * A Programmer can offer a daily, short (e.g., a 10-minute preview) of one of their sites.
    * A Programmer can offer a single, long presentation (e.g., four-hours) of a major sporting event such as the Olympics, or NCAA March Madness.  
    * A Programmer can provide a combination of the previous two scenarios; for example, an initial, longer viewing period one day, followed by a series of short periods that repeat daily for some number of subsequent days. 
*   Programmers specify the duration (Time-To-Live, or TTL) of their Temp Pass.  
*   Temp Pass operates per requestor.  For example, NBC could set up a 4-hour Temp Pass for the requestor "NBCOlympics".
*   Programmers can reset all of the tokens granted to a particular requestor.  The "temporary MVPD" used to implement the Temp Pass must be configured with "Authentication Per Requestor" enabled.  
*   **Temp Pass access is granted to individual users on specific devices**. After Temp Pass access expires for a user, that user will not be able to get temporary access on the same device until that user's expired [authorization token](/help/authentication/glossary.md#authz-token) is cleared from the Adobe Primetime authentication server.
 

>[!NOTE]
>
>Temp Pass is part of the Premium Workflow package. Please contact your Primetime sales rep if interested in using this functionality.

## Feature details {#tempass-featur-details}

*   **How Viewing Time Is Computed** - The amount of time that a Temp Pass remains valid does not correlate to the amount of time a user spends viewing content on the Programmer's application.  Upon the initial user request for authorization via Temp Pass, an expiration time is computed by adding the initial current request time to the TTL specified by the Programmer. This expiration time is associated with the user's device ID and Programmer's requestor ID, and stored in the Primetime authentication database. Each time the user tries to access content using Temp Pass from the same device, Primetime authentication will compare the server request time with the expiration time associated with the user's device ID and the Programmer's requestor ID. If the server request time is less than the expiration time, the authorization will be granted; otherwise, the authorization will be denied. 
*   **Configuration Parameters** - The following Temp Pass parameters can be specified by a Programmer to create a Temp Pass rule:
    * **Token TTL** - The amount of time that a user is allowed to watch without signing in to an MVPD. This time is clock-based, and expires whether the user is watching content or not.
    >[!NOTE]
    >A requestor ID cannot have more than one Temp Pass rule associated with it.  
*   **Authentication / Authorization** - In the Temp Pass flow, you specify the MVPD as "Temp Pass".  Primetime authentication does not communicate with an actual MVPD in the Temp Pass flow, so the "Temp Pass" MVPD authorizes any resource. Programmers can specify a resource that is accessible using Temp Pass just as they do for the rest of the resources on their site. The Media Verifier Library can be used as per usual to verify the Temp Pass short media token and enforce resource checking before playback.
*   **Tracking Data in Temp Pass Flow** - Two points regarding tracking data during a Temp Pass entitlement flow:
    * The Tracking ID that is passed from Primetime authentication to your **sendTrackingData()** callback is a hash of the Device ID.
    * Since the MVPD ID used in the Temp Pass flow is "Temp Pass", that same MVPD ID is passed back to **sendTrackingData()**. Most Programmers will likely want to treat Temp Pass metrics differently than actual MVPD metrics. This requires some additional work in your analytics implementation. 

The following illustration shows the Temp Pass flow:

![The Temp Pass flow](assets/temp-pass-flow.png)

*Figure: The Temp Pass flow*

## Implement Temp Pass {#implement-tempass}

On the Primetime authentication side, Temp Pass is implemented with the addition of a pseudo-MVPD named "TempPass" to the participating Programmer's server configuration.  This pseudo-MVPD acts like an actual MVPD that temporarily grants access to the Programmer's protected content. 

On the Programmer side, Temp Pass is implemented as follows for the two scenarios that MVPDs use for authentication:

* **iFrame on Programmer's page**. Temp Pass works regardless of an MVPD's authentication type, but for the iFrame scenario additional steps are required to cancel the current authentication flow and authenticate with Temp Pass. These steps are shown in the [iFrame Login](/help/authentication/temp-pass.md) below.
* **Re-direct to MVPD login page**. In the more traditional case where the UI for triggering the Temp Pass is presented prior to starting authentication with an MVPD, there are no special steps to be taken. Temp Pass should be treated just like a regular MVPD.

The following points apply to both implementation scenarios:

* The "Temp Pass" should be displayed in the MVPD picker only for users who haven't yet requested a Temp Pass authorization. Blocking the display for subsequent requests can be achieved by keeping a flag on cookies. This will work as long as the user does not clear the browser cache. If users clear their browser caches, "Temp Pass" appears again in the picker, and the user will be able to request it again. Access will be granted only if the "Temp Pass" time has not expired yet. 
* When a user requests access via Temp Pass, the Primetime authentication Server will not perform its usual Security Assertion Markup Language (SAML) request during the authentication process. Instead, the authentication endpoint will return success every time it is invoked while tokens are valid for the device. 
* When a Temp Pass expires, its user will not be authenticated anymore, because in the Temp Pass flow the authentication token and the authorization token have the same expiration date. In order to explain to users that their Temp Pass has expired, Programmers must retrieve the selected MVPD right after calling `setRequestor()`, and then call `checkAuthentication()` as per usual. In the `setAuthenticationStatus()` callback a check can be made to determine if auth status is 0, so that if the selected MVPD was "TempPass" a message can be presented to users that their Temp Pass session has expired.  
* If a user deletes the Temp Pass token prior to expiration, the subsequent entitlement checks will generate a token that will have a TTL equal to the remaining time.
* If the user deletes the Temp Pass token after expiration, the subsequent entitlement checks will return "user not authorized".
 
See the samples in [Sample Code](/help/authentication/temp-pass.md#tempass-sample-code) below for examples of how to code the implementation details described in this section.

## Sample code {#tempass-sample-code}

The sections below show how to call the Primetime authentication API to implement the Temp Pass flow:

* [iFrame login sample](/help/authentication/temp-pass.md#iframe-login-sample)
* [Auto login sample](/help/authentication/temp-pass.md#auto-login-sample)

### iFrame login sample {#iframe-login-sample}

This example shows how to implement Temp Pass for the case where MVPDs support iFrame integration:

```HTML

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>

```

#### iFrame login use cases {#iframe-login-use-cases}

**To request a Temp Pass for the first time:**

1. A user accesses the Programmer's page and clicks the sign-in link.
1. The MVPD picker opens and the user chooses an MVPD from the list.
1. The authentication iFrame is displayed. This iFrame contains a "Temp Pass" link.
1. The user clicks "Temp Pass", so the Programmer adds a flag to a cookie to prevent the user from seeing the "Temp Pass" link on subsequent visits to the page.
1. The Temp Pass authentication request reaches the Primetime authentication servers, and they generate an authentication token. The TTL is equal to the time period set by the Programmer for the Temp Pass.
1. The Temp Pass authorization request reaches the Primetime authentication servers.
1. The Primetime authentication servers extract the device and requestor IDs from the request, and store them in the database together with the expiration time. The expiration time is calculated as: initial Temp Pass request time plus the TTL (specified by the Programmer).
1. The Primetime authentication servers generate an authorization token.
1. The user accesses the protected content.

**To requesting a Temp Pass again after a returning Temp Pass user has deleted the browser cookies:**

1. The user accesses the Programmer's page and clicks the sign-in link.
1. The MVPD picker opens and the user chooses an MVPD from the list.
1. The authentication iFrame is displayed. This iFrame contains a "Temp Pass" link (the user deleted the original cookie, so the Programmer doesn't know if the user has clicked on the "Temp Pass" link before).
1. The user clicks on "Temp Pass" again, so the Programmer adds a flag to a cookie again, to prevent the user from seeing the "Temp Pass" link on subsequent visits to the page.
1. The Temp Pass authentication request reaches the Primetime authentication servers, which generate an authentication token. The TTL is now the remaining time for the Temp Pass (the difference between the current time and the expiration time associated with the device ID).
1. The Temp Pass authorization request reaches the Primetime authentication servers.
1. The Primetime authentication servers extract the device and requestor IDs from the request, and use them to retrieve the expiration time from the Primetime authentication database. The current time is compared to the expiration time.
1. If the user's Temp Pass has not expired, the Primetime authentication servers generate an authorization token.
1. If the user's Temp Pass has not expired, the user will be able to access the protected content.

### Auto login sample {#auto-login-sample}

The following sample illustrates a case where a user is automatically logged in with TempPass when visiting a site. The user can choose to login with a regular MVPD at any time, and is warned if TempPass has expired:

```HTML

<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## Use multiple Temp Passes {#use-mult-tempass}

Certain events require phased free access to content, such as an initial interval of free access (e.g., 4 hours), followed by daily free accesses (e.g., 10 minutes on each subsequent day).  In order for a Programmer to implement this scenario, they must arrange it with their Adobe contact to configure two temporary MVPDs for the Programmer. 

For this example scenario (an initial 4 hours free session, followed by daily 10 minute free sessions) Adobe configures an MVPD called TempPass1 with a Time-To-Live (TTL) of 4 hours, and a TempPass2 with a TTL of 10 minutes for the subsequent period.  Both of these are associated with the Programmer's Requestor ID.

### Programmer implementation {#mult-tempass-prog-impl}

After Adobe configures the two TempPass instances, the two additional MVPDs (TempPass1 and TempPass2), will appear in the Programmer's MVPD list.  The Programmer needs to take the following steps to implement the multiple temp passes:

1. On the user's initial visit to the site, automatically log them in with TempPass1. You can use the Autologin Sample above as a starting point for this task.
1. When you detect that TempPass1 has expired, store the fact (in a cookie/local storage) and present the user with your standard MVPD picker. **Make sure to filter out TempPass1 and TempPass2 from that list**.
1. On each subsequent day, if TempPass1 is expired, autologin that user with TempPass2.
1. When TempPass2 is expired, store the fact (in a cookie/local storage) for the day, and present the user with your standard MVPD picker. Again, make sure to filter out TempPass1 and TempPass2 from that list.
1. On each new day, at 00:00 hours, reset all temp passes for TempPass2, using the [Reset TempPass web API](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**Programming note:** Primetime Authentication does not have a built-in mechanism to stop the free streaming after the 10 minutes has passed.  It is up to Programmers to restrict the access once TempPass2 expires. To accomplish this, Programmers can implement in their sites/apps a "checkAuthorization" call every X minutes, where X is the time period that the Programmer determines makes sense for their apps.

## Reset all Temp Passes {#reset-all-tempass}

Certain business rules require regular purging of Temp Pass, or an ad hoc reset of all Temp Passes issued for a particular Requestor ID and MVPD ID. This feature supports use cases such as the following:

* A daily 10-minute Temp Pass (the Temp Pass must be reset at the beginning of the day)
* A Temp Pass available for all users during breaking news. (The Temp Pass needs to be reset for all devices as soon as the breaking news starts.)
* The multiple Temp Pass scenario that provides a combination of an initial viewing period of some length, followed by subsequent daily periods of another length.
 
In order to reset all Temp Passes, Primetime authentication provides Programmers with a *public* web API:

```url

DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset

```

>[!NOTE]
>The URL above supersedes the previous reset API. The old reset API (v1) is no longer supported.

*   **Protocol:** HTTPS
*   **Host:**
    * Release - mgmt.auth.adobe.com
    * Prequal - mgmt-prequal.auth.adobe.com
*   **Path:** /reset-tempass/v2/reset
*   **Query parameters:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
*   **Headers:** ApiKey - 1232293681726481
*   **Response:** 
    *   Success - HTTP 204
    *   Failure:
        * HTTP 400 for an incorrect request
        * HTTP 401 if the ApiKey was not specified
        * HTTP 403 if the ApiKey is invalid

For example:

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"

```

## Supported clients {#supp-clients}

Temp Pass and Reset Tool support by platform:

| Adobe Primetime authentication Clients | Temp Pass | Reset Tool |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler                       | YES       | YES        |
| Native Client iOS                      | YES       | YES        |
| Native Client tvOS                     | YES       | YES        |
| Native Client Android                  | YES       | YES        |
| Native Client fireTV                   | YES       | YES        |
| Clientless API                         | YES       | YES        |

## Limitations and known issues {#limitations}

This section describes the limitations that apply to the current implementation of Temp Pass. 

**JavaScript SDK**: supports reset temp pass functionality from version **3.X and above**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->
