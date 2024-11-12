---
title: REST API V2 Cookbook (Server-to-Server)
description: REST API V2 Cookbook (Server-to-Server)
exl-id: 3160c03c-849d-4d39-95e5-9a9cbb46174d
---
# REST API V2 Cookbook (Server-to-Server) {#rest-api-v2-cookbook-server-to-server}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

The purpose of this cookbook document is to detail best practices for implementing Adobe Pass Authentication using the REST API V2 in a Server-to-Server architecture. It provides basic requirements, step-by-step flow implementation and general considerations for production environments and operation.

## Components {#components}

In a working Server-to-Server solution, the following components are involved:

| Type                      | Component                 | Description                                                                                                                                                                                      |
|---------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Streaming Device          | Streaming App             | The Programmer application that resides on the user's streaming device and plays authenticated video.                                                                                            |
|                           | \[Optional\] AuthN Module | If Streaming Device has a User Agent (i.e. Web Browser), the AuthN Module is responsible for authenticating the user on the MVPD IdP.                                                            |
| \[Optional\] AuthN Device | AuthN App                 | If the Streaming Device does not have a User Agent (i.e. Web Browser), the AuthN Application is a Programmer web application that is accessed from a separate user's device using a web browser. |
| Programmer Infrastructure | Programmer Service        | A service that links the Streaming Device with the  Adobe Pass Service to obtain authentication and authorization decisions.                                                                     |
| Adobe Infrastructure      | Adobe Pass Service        | A service that integrates with the MVPD IdP and AuthZ Service and provides authentication and authorization decisions.                                                                           |
| MVPD Infrastructure       | MVPD IdP                  | An MVPD endpoint that provides credential-based authentication service to validate their user's identity.                                                                                        |
|                           | MVPD AuthZ Service        | An MVPD endpoint that provides authorization decisions based on user's subscriptions, parental controls, etc.                                                                                    |

Additional terms used in the flow are defined in the [Glossary](/help/authentication/glossary.md).

The following diagram illustrates the entire flow:

![REST API V2 Cookbook (Server-to-Server)](/help/authentication/assets/rest-api-v2/cookbooks/rest-api-v2-cookbook-server-to-server-diagram.png)

### Steps to implement the REST API V2 in server-to-server architecture {#steps-to-implement-the-rest-api-v2-in-server-to-server-infrastructure}

To implement Adobe Pass REST API V2, you need to follow the steps below grouped into phases.

## 0. Prerequisites {#prerequisites}

In Server-to-Server implementations, the Streaming App and Programmer Service needs to establish a protocol for Programmer Service to be able to:

* Uniquely identify the Streaming App on the device.
* Act on behalf of the Streaming App and communicate with Adobe Pass Service.
* Collect and store information about the Streaming App and the device like IP address, source port, device information to pass it to Adobe Pass.
* Return decisions and instructions to the Streaming App.

Parameters like device ID, client id, client secret (defined below) can be stored on either Streaming App or Programmer Service.

## A. Registration phase {#registration-phase}

### Step 1: Register your application {#step-1-register-your-application}

For the application to be able to call Adobe Pass REST API V2, it needs an access token required by the API security layer. 

For Server-to-Server implementations, the Programmer Service can register on behalf of an application instance, yet the client credentials (client id and client secret) values need to be obtained for each streaming device. 

To get the access token, the Programmer Service can act on behalf of a Streaming App and needs to follow steps as described in the [Dynamic Client Registration](../../dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md) documentation.

## B. Authentication phase {#authentication-phase}

### Step 2: Check for existing authenticated profiles {#step-2-check-for-existing-authenticated-profiles}

The Programmer Service checks on behalf of the Streaming App for existing authenticated profiles: `/api/v2/{serviceProvider}/profiles` ([Retrieve authenticated profiles](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)).

* If no profile found and Streaming application implements a TempPass flow
    * Follow documentation on how to implement [Temporary access flows](../flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md)
* If no profile found, Streaming application implements an Authentication flow
    * <b>Step 2.a:</b> the Programmer Service retrieve the list of MVPDs available for serviceProvider: <b>/api/v2/{serviceProvider}/configuration</b><br>
      ([Retrieve list of available MVPDs](../apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md))
    * The Programmer Service may implement filtering on the list of MVPDs and display only MVPDs intended while hiding others (TempPass, test MVPDs, MVPDs under development, etc.)
    * The Programmer Service should return a filtered MVPD list for the Streaming App to display picker, User selects the MVPD
    * With the MVPD selected from Streaming App, the Programmer Service creates a session: <b>/api/v2/{serviceProvider}/sessions</b><br>
      ([Create authentication session](../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md))<br>
        * A CODE and URL to use for authentication is returned
        * If a profile is found, the Programmer Service may proceed to <a href="#preauthorization-phase">C. Preauthorization phase</a>
    * The Programmer Service should return the CODE and URL to the Streaming App
  
### Step 3: Authenticate the user {#step-3-authenticate-the-user}

Using a Browser or a Second Screen Web-based application:

* Option 1. Streaming App can open a browser or webview, load the URL to authenticate, and the user lands on MVPD login page where credentials need to be submitted
    * User enters login/password, final redirect shows a success page
* Option 2. Streaming App can't open a browser and just display the CODE. <b>A separate web application, AuthN_APP, needs to be developed</b> to ask the user to enter CODE, build and open URL: <b>/api/v2/authenticate/{serviceProvider}/{CODE}</b>
    * User enters login/password, final redirect shows a success page

### Step 4: Check for authenticated profiles {#step-4-check-for-authenticated-profiles}

The Programmer Service checks for authentication with MVPD to complete in Browser or Second Screen

* Polling every 15 seconds is recommended on <b>/api/v2/{serviceProvider}/profiles/{mvpd}</b><br>
  ([Retrieve authenticated profiles for specific MVPD](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md))
    * If MVPD selection is not made in the Streaming application as the MVPD picker is presented in the Second Screen application, the polling should happen with CODE <b>/api/v2/{serviceProvider}/profiles/code/{CODE}</b><br>
      ([Retrieve authenticated profiles for specific CODE](../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md))
* Polling should not exceed 30 minutes, in case 30 minutes are reached, and the Streaming Application is still active, a new session needs to be initiated and a new CODE and URL will be returned
* When authentication is complete, the return is 200 with authenticated profile
* The Programmer Service may proceed to <a href="#preauthorization-phase">C. Preauthorization phase</a>

## C. Preauthorization phase {#preauthorization-phase}

### Step 5: Check for preauthorized resources {#step-5-check-for-preauthorized-resources}

With a valid authentication profile for a user, the Programmer Service has the possibility to check the access to the videos available and pass the list to the Streaming Application to display.

* Step is optional and executed if the application wants to filter out the resources not available in the authenticated user package
* Call to <b>/api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}</b><br>
  ([Retrieve preauthorization decision using specific MVPD](../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md))

## D. Authorization phase {#authorization-phase}

### Step 6: Check for authorized resources {#step-6-check-for-authorized-resources}

Streaming App prepares to play a video/asset/resource selected by the user.

* Step is necessary for every play start
* Streaming App passes this information to the Programmer Service
* The Programmer Service on behalf of the Streaming App, call <b>/api/v2/{serviceProvider}/decision/authorize/{mvpd}</b><br>
  ([Retrieve authorization decision using specific MVPD](../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md))
    * decision = 'Permit', Programmer Service instructs the Streaming App to start streaming
    * decision = 'Deny', Programmer Service instructs the Streaming App to inform the user that it does not have access to that video
    * in the process, the Programmer Service may evaluate other business rules and return appropriate decision to the Streaming App

## E. Logout phase {#logout-phase}

### Step 7: Logout {#step-7-logout}

Streaming App: User wants to log out from the MVPD

* Streaming App informs the Programmer Service that it needs to log out from the MVPD for this specific App.
* The Programmer Service may clean up the information it stores about the authenticated user
* The Programmer Service call <b>/api/v2/{serviceProvider}/logout/{mvpd}</b><br>
  ([Initiate logout for specific MVPD](../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md))
* If the response actionType='interactive' and url is present, the Programmer Service will return to the Streaming App the url 
* Based on existing capabilities, the Streaming App may open the url in the browser (usually the same one as used for authentication)
* If the Streaming App does not have a browser, or it is a different instance than the one at authentication, the flow can be stopped as the MVPD session was not persisted in the browser cache. 

## Environments and Functional Requirements{#environments}

A Programmer should create at least two environments: one for production, and one or more for staging.

### Production

The production environment should be highly available and scaled appropriately for large or unexpected spikes (e.g., live sports, breaking news).

The Adobe Pass Service runs on multiple data centers geographically dispersed throughout the US. To achieve the best response time (i.e., the lowest latency) from the Adobe Pass service, the Programmer should also create a similar geographically dispersed service infrastructure.

The Programmer Service should limit the DNS cache to a maximum of 30s in case Adobe needs to reroute traffic. This may occur if a data center becomes unavailable.

The Programmer should provide the public IP range of the production environment. These will be entered into an allowed-list of IPs in Adobe Pass infrastructure for access and managed by Adobe's Fair API usage policies.

### Staging

The staging environment can be minimal, but should include all system components and business logic. It should function similarly to production and allow for testing releases outside of production. Ideally, the staging environment can be connected to the Adobe Pass testing environments for use by the Programmer, and by Adobe when needed, so we can help in testing and troubleshooting.

### Functional Requirements

The Programmer Service must pass along accurate device identification information for the device for which they are executing the flows. Additionally, the Programmer service must pass the IP of the device for which they are executing the flows (in an x-forwarded-for header) along with the connection source port (in the device info field):

The Programmer Service should send data and formating required by individual MVPDs or integrated apps (e.g., device IP, source port, device information, MRSS, optional data such as ECID). <!--Please see the documentation for [Passing Device and Connection Information Cookbook](http://tve.helpdocsonline.com/passing-device-information-cookbook)-->.

The Programmer Service must respect authentication profile and decisions validity when caching and invalidate the authentications or decisions when notified.

The Programmer Service must maintain certificates shared with Adobe (for encrypted user metadata).

## Related Information {#related}

* [REST API V2 Reference](/help/authentication/rest-api-v2/rest-api-v2-overview.md)
