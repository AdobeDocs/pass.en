---
title: REST API V2 Cookbook (Client-to-Server)
description: REST API V2 Cookbook (Client-to-Server)
exl-id: 6a5a89d2-ea54-4f9c-9505-e575ced4301c
---
# REST API V2 Cookbook (Client-to-Server) {#rest-api-v2-cookbook-clientserver}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

## Steps to implement the REST API V2 in client side applications {#steps-to-implement-the-rest-api-v2-in-client-side-applications}

To implement Adobe Pass REST API V2, you need to follow the steps below, grouped into phases.

## A. Registration phase {#registration-phase}

### Step 1: Register your application {#step-1-register-your-application}

For the application to be able to call Adobe Pass REST API V2, it needs an access token required by the API security layer.

To get the access token, the application needs to follow steps as described: [Dynamic Client Registration](../../dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md)

## B. Authentication phase {#authentication-phase}

### Step 2: Check for existing authenticated profiles {#step-2-check-for-existing-authenticated-profiles}

Streaming application checks for existing authenticated profiles: <b>/api/v2/{serviceProvider}/profiles</b><br>
([Retrieve authenticated profiles](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md))

* If no profile is found and the Streaming application implements a TempPass flow 
  * Follow documentation on how to implement [Temporary access flows](../flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md)
* If no profile is found and the Streaming application implements an Authentication flow
  * Streaming application retrieves the list of MVPDs available for serviceProvider: <b>/api/v2/{serviceProvider}/configuration</b><br> 
  ([Retrieve list of available MVPDs](../apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md))
  * Streaming application may implement filtering on the list of MVPDs and display only MVPDs intended while hiding others (TempPass, test MVPDs, MVPDs under development, etc.) 
  * Streaming application displays picker, User selects the MVPD
  * Streaming application creates a session: <b>/api/v2/{serviceProvider}/sessions</b><br>
  ([Create authentication session](../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md))<br>
    * a CODE and URL to use for authentication is returned
    * if a profile is found, Streaming application may proceed to <a href="#preauthorization-phase">C. Preauthorization phase</a> or <a href="#authorization-phase">D. Authorization phase</a>

### Step 3: Authenticate the user {#step-3-authenticate-the-user}

Using a Browser or a Second Screen Web based application:

* Option 1. Streaming Application can open a browser or webview, load the URL to authenticate and the user lands on the MVPD login page where credentials need to be submitted
  * user enters login/password, final redirect shows a success page
* Option 2. Streaming Application can't open a browser and just display the CODE. <b>A separate web application needs to be developed</b> to asks the user to enter CODE, build and open URL : <b>/api/v2/authenticate/{serviceProvider}/{CODE}</b>
  * user enter login/password, final redirect show a success page

### Step 4: Check for authenticated profiles {#step-4-check-for-authenticated-profiles}

Streaming application checks for authentication with MVPD to complete in Browser or Second Screen

* Polling every 15 seconds is recommended on <b>/api/v2/{serviceProvider}/profiles/{mvpd}</b><br>
([Retrieve authenticated profiles for specific MVPD](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md))
  * If MVPD selection is not made in the Streaming application as the MVPD picker is presented in the Second Screen application, the polling should happen with CODE <b>/api/v2/{serviceProvider}/profiles/code/{CODE}</b><br>
    ([Retrieve authenticated profiles for specific CODE](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md))
* Polling should not exceed 30 minutes, in case 30 minutes are reached and the Streaming Application is still active, a new session needs to be initiated and a new CODE and URL will be returned
* When authentication is complete, the return is 200 with authenticated profile
* The Streaming application may proceed to <a href="#preauthorization-phase">C. Preauthorization phase</a> or <a href="#authorization-phase">D. Authorization phase</a>

## C. Preauthorization phase {#preauthorization-phase}

### Step 5: Check for preauthorized resources {#step-5-check-for-preauthorized-resources}

Streaming application prepares to display the videos available for the authenticated user and has the possibility to check the
access to these resources.

* Step is optional and executed if the application wants to filter our the resources not available in the authenticated user package
* Call to <b>/api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}</b><br>
([Retrieve preauthorization decision using specific MVPD](../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md))

## D. Authorization phase {#authorization-phase}

### Step 6: Check for authorized resources {#step-6-check-for-authorized-resources}

Streaming application prepares to play a video/asset/resource selected by the user.

* Step is necessary for every play start
* Call <b>/api/v2/{serviceProvider}/decision/authorize/{mvpd}</b><br>
([Retrieve authorization decision using specific MVPD](../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md))
  * decision = 'Permit' , Streaming device starts streaming
  * decision = 'Deny', Streaming device informs the user that it does not have access to that video

## E. Logout phase {#logout-phase}

### Step 7: Logout {#step-7-logout}

Streaming device: User wants to logout from the MVPD

* Call <b>/api/v2/{serviceProvider}/logout/{mvpd}</b><br>
([Initiate logout for specific MVPD](../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md))
* If the response actionType='interactive' and url is present, open the url in a Browser/Second Screen to complete logout with MVPD
