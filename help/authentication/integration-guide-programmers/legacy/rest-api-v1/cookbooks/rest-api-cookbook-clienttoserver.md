---
title: REST API Cookbook (Client-to-Server)
description: Rest API cookbook client to server.
exl-id: f54a1eda-47d5-4f02-b343-8cdbc99a73c0
---
# (Legacy) REST API Cookbook (Client-to-Server) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Overview {#overview}

This document provides step-by-step instructions for a Programmer's engineering team to integrate a "smart device" (game console, smart TV app, set top box, etc.) with Adobe Pass Authentication using REST API services. This Client-to-Server approach, which uses REST APIs rather than a client SDK, allows for broader support of different platforms for which developing a significant number of unique SDKs would not be feasible. For a broad technical overview of how the Clientless solution works, see the [Clientless Technical Overview](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/rest-api-overview.md).


This approach requires two components (streaming app and AuthN app) to complete the required flows: start-up, registration, authorization, and view-media flows in the streaming app, and the authentication flow in your AuthN app.

### Throttling mechanism

The Adobe Pass Authentication REST API is governed by a [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md).

## Components {#components}

In a working Client-to-Server solution the following components are involved:

 

| Type | Component | Description |
| --- | --- | --- |
| Streaming Device | Streaming App | The Programmer application that resides on the user's streaming device and plays authenticated video. |
| | \[Optional\] AuthN Module | if Streaming Device has a User Agent (i.e. Web Browser), the AuthN Module is responsible for authenticating the user on the MVPD IdP. |
| \[Optional\] AuthN Device | AuthN App | if the Streaming Device does not have a User Agent (i.e. Web Browser), the AuthN Application is a Programmer web application that is accessed from a separte user's device using a web browser. |
| Adobe Infrastructure | Adobe Pass Service | A service that integrates with the MVPD IdP and AuthZ Service and provides authentication and authorization decisions. |
|  MVPD Infrastructure | MVPD IdP | An MVPD endpoint that provides credential-based authentication service to validate their user's identity. | 
| | MVPD AuthZ Service | An MVPD endpoint that provides authorization decisions based on user's subscriptions, parental controls, etc. |

 

Additional terms used in the flow are defined in the [Glossary](/help/authentication/kickstart/glossary.md).

## Flows{#flows}

### Dynamic Client Registration (DCR)

Adobe Pass uses DCR to secure client communications between a programmer application or server and the Adobe Pass services. The DCR flow is separate and is described in the [Dynamic Client Registration Overview](../../../rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.


### Streaming  (Smart Device) App Flows

![](../../../../assets/smart-device-app-flow.png)

#### Startup Flow

1.  Your app starts and loads its initial UI.

2.  Obtain / generate a device ID.

3.  Issue a Check-authentication call to see if the device is already authenticated.  For example: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md)

4.  If the `checkauthn` call succeeds, proceed to the Authorization Flow from Step 2 onwards.  If it fails, start the Registration Flow.

 

#### Registration Flow

1.  Get a registration code and URL for your user to use to access your 2nd screen login app, and present these to the user:
    
    a.  Send a POST request to the Adobe Registration Code Service, passing a hashed device ID and a "Registration URL".  For example: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md)
    
    b.  Present the returned registration code and URL to the user.
    
    c.  Instruct the user to switch to a web-capable device, navigate to the URL, and then enter the registration code.

 

#### Authorization Flow

1.  The user returns from the 2nd screen app and presses the "Continue" button on your device. Alternatively, you could implement a polling mechanism to check the authentication status, but the Adobe Pass Authentication recommends the Continue button method over polling. <!--(For information on employing a "Continue" button versus polling the Adobe Pass Authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> For example: [\<SP\_FQDN\>/api/v1/tokens/authn](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md)

2.  Send a GET request to the Adobe Pass Authentication authorization service to initiate authorization. For example: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

* If the response indicates success: The user has a valid AuthN token AND the user is authorized to watch the requested media (there is a valid AuthZ token for this user).

* If the response indicates failure: Examine the Exception thrown to determine its type (AuthN, AuthZ, or something else):
  
  * If it was an AuthN error then re-start the Registration Flow.

  * If it was an AuthZ error then the user is not authorized to watch the requested media and some kind of error message should be displayed to the user.

  * If there was some other error (connection error, network error, etc.) then display an appropriate error message to the user.

 

#### View Media Flow

1.  Present media choices. The user selects the media to view.

2.  Is the media protected?
    
    a.  Your app checks if the media is protected.
    
    b.  If the media is protected, your app starts the Authorization
        (AuthZ) Flow above.
    
    c.  If the media is not protected, then playback the media for the
        user.

3.  Playback the media.


### AuthN (2nd Screen) App Flow

![](../../../../assets/secnd-screen-authn-flow.png)

1.  Get a list of MVPDs for this user. For example: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/provide-mvpd-list.md)

1.  Initiate the authentication flow.  For example: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)

1.  Check whether the authentication was successful. For example:[`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md)

1.  Send the user back to your Smart Device app to complete the authorization flow.

## Partner Single Sign-On {#partner-sso}

Some devices provide dedicated support for Partner Single Sign-On (SSO):

* [Apple SSO](/help/authentication/integration-guide-programmers/legacy/sso-access/apple-sso-cookbook-rest-api-v1.md)

## Platform Single Sign-On {#platform-sso}

Some devices provide dedicated support for Platform Single Sign-On (SSO):

* [Amazon SSO](../../sso-access/amazon-sso-cookbook-rest-api-v1.md)
* [Roku SSO](../../../features-standard/sso-access/platform-sso/roku-single-sign-on/roku-sso-overview.md)

## TempPass and Promotional TempPass for REST API {#temppass}

For TempPass and Promotional TempPass implementations where the user is not required to enter credentials, authentication can be implemented directly in the Streaming App.

**In order to use this API the Streaming App needs to make sure of the uniqueness of the device ID as this is being used for identifying the token, along with the optional extra data.**


![](../../../../assets/temp-pass-promo-temppass.png)
