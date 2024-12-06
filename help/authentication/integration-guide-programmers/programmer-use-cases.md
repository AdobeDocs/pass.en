---
title: Programmer use cases
description: Programmer use cases
exl-id: 51ca7e4f-b0d8-4e35-8398-2efb4879de2a
---
# Programmer use cases {#programmer-use-cases}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

This document summarizes the Programmer integration use cases supported by Adobe Pass Authentication. You can check this page before beginning an integration project to see which features are currently supported.

## Use cases {#use-cases}


### Basic integration: Federated authentication and authorization for a single channel network {#basic-integration}

**Priority** - High

**Breakdown** -  Single Programmer-branded TVE app with 1 Channel Network hosted inside the experience

This enables Programmers to offer premium content, in their own branded TVE app*, with a federated entitlement check to the MVPD. The requestorID should align to match the brand of the application serving the content to the viewer. In this scenario, there is a 1 to 1 relationship between the Adobe Pass Authentication Requestor ID and the Resource ID that gets verified for entitlement.

>[!NOTE]
>
>TVE app is used in this document to refer collectively to the different types of applications (web apps, mobile apps, etc.) supported by Adobe Pass Authentication. The Platforms column below may contain details about supported platforms for specific use cases.

#### Specific use cases (common to most integrations) {#sp-use-cases-basic-int}

| Priority |                        Use Case                       |                                                                                                                                                                    Description                                                                                                                                                                   |                                   Platforms                                  |                 MVPD Notes                |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| High     | MVPD Discovery From Programmer TVE App                | The user starts on the Programmer's branded TVE app and is prompted to select their MVPD Provider.                                                                                                                                                                                                                                               |                                 Web (SWF/JS)                    Mobile (iOS/Android)                   Clientless API (for 2nd-Screen)                           |                                           |
| High     | Federated Authentication From the Programmer TVE App  | The user starts on the Programmer's branded  TVE app and after selecting their MVPD Provider, the user is  transitioned to the MVPD's own login page to enter their credentials.                                                                                                                                                                 |                                 Web (SWF/JS)                    Mobile (iOS/Android)                                                             |                                           |
| High     | Authorization From Programmer TVE App                 |               After the user is authenticated, the Programmer's TVE app is able  to make back-channel authorization requests to the MVPD to check the  user's entitlement. Usually this is just checking whether the Channel  Network is in the users MVPD subscription package.                                  In this case, the Requestor ID and Resource ID will match up 1:1.              | All platforms                                                                |                                           |
| Medium   | Logout From Programmer TVE App                        | Enables the user to logout and clear the  Adobe Pass Authentication AuthN/AuthZ tokens. In many cases, this  also logs the user out from the MVPD as well. But MVPDs vary in whether  this is supported. It always clears the Adobe Pass Authentication  session and tokens.                                                           | All platforms except XBox Native                                             | Several MVPDs don't support this.         |
| High     | Single Sign-On Across Sites and Apps                  | Enables the user to share the login session across sites and apps without need to log in again.                                                                                                                                                                                                                                                  | All platforms except Clientless API                                          | Requires at least SDK 1.7 for some MVPDs. |

### Single TVE app hosting multiple channel networks {#single-app-multi-channel}

**Priority**- High

Enables the Programmer to aggregate several channel networks of content on the same branded destination for their viewers.

#### Specific use cases {#sp-use-cases-singl-tve-app}

| Priority |            Use Case            |                                                                                                                  Description                                                                                                                  |   Platforms   |                                                                                                                                                                                                                                       MVPD Notes                                                                                                                                                                                                                                      |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| High     | Distinct Channel Authorization | The user is able to watch content from  several channel networks inside the same TVE app. The Programmer is able  to make authorization calls that are specific to each channel network  to confirm the users' entitlement.                   | All platforms | All MVPDs now support this in some form.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Low      | Preflight Authorization Query  | This enables the Programmer to check which  channels the user has in their package in a single API call. This is  done before actual AuthZ calls to filter content out of the user  interface that the user doesn't have access to.                                                           |               | Most MVPDs don't yet expose this data as  User Attributes, so Adobe actually makes AuthZ calls to get it. Also,  most MVPDs are limited to 5 at a time, because they don't support  multiple channels in a single call.                             It's very important to verify how many channels the Programmer needs  to preflight check. No matter what the number is, we'll need to check  that it is ok with the MVPDs. Most MVPDs do not currently (3rd Quarter,  2013) support more than 5 channels. |

### Asset level authorization {#asset-level-authz}

**Priority** - Low

**Breakdown** - Pass An Asset Identifier On Authorization Request

**Platforms** - All platforms

#### Specific use cases {#sp-use-cases-asset-lvl-authz}

Enables the MVPD to get asset level analytics on each AuthZ call. This has the disadvantage of negating the Adobe Pass Authentication AuthZ cache.

| Priority |                      Use Case                     |                                                                    Description                                                                   |   Platforms   |               MVPD Notes               |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Low      | Pass an Asset Identifier on Authorization Request | Enables the MVPD to get asset level analytics on each AuthZ call.  Has the downside of negating the Adobe Pass Authentication AuthZ  cache. | All platforms | Only one MVPD supports this currently. |




### Parental controls {#parental-controls}

**Priority** - Low

Enables MVPD user account restrictions to be applied on the Programmer's TVE app.

| Priority |                  Use Case                 |                                                                                               Description                                                                                              |                   Platforms                  |              MVPD Notes             |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Low      | Filter Content Based on User Attributes   | Enables the Programmer to check Max Rating allowed for a user before rendering the list of available content to the user.                                                                              |                                 Web (Flash/JS)                    Mobile (iOS/Android)                           | Only works with one MVPD currently. |
| Low      | Pass Content Ratings in the AuthZ Request | Enables the Programmer to pass the specific rating of the content  the user wants to watch as part of the AuthZ request to the MVPD                             Related to #3, since ratings are typically at the asset level. | All platforms                                | Only works with one MVPD currently. |

#### MVPD integration customization per programmer brand {#mvpd-int-cust-prog-brand}

**Priority** - Medium

Enables custom experience during AuthN or for AuthZ error messages.

| Priority |                        Use Case                        |                                                                                        Description                                                                                       |     Platforms     |                 MVPD Notes                |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Medium   | Pass Service Provider Identifier in the AuthN Request. | Enable specific branding on the MVPD login page specific to the  service provider. Also enable automatically selecting the default to  match the audience such as Spanish for Univision. | All platforms     | Varies by MVPD. Some do not support this. |
| Medium   | Custom Error Messages on AuthZ Response                | Enables Programmer or brand specific error messages from the MVPD  that can include specific message for upsell with a link that upgrade  the package.                                   | Web, Android, iOS | Varies by MVPD. Some do not support this. |


### Connected device use cases {#connected-devices}

| Priority |                            Use Case                           |                                                        Description                                                       |    Platforms    |                                                                                  MVPD Notes                                                                                  |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medium   | XBox LiveID SSO Across Apps and Consoles                      | Enables the user to share AuthN session between apps and between different game consoles - tied to their LiveID account. | XBox Native SDK | Most MVPDs don't like this because the typical model is to bind the token to the device - not to the user.                             We don't recommend this approach anymore if at all possible.  |
| High     | Connected Device With Tokens Bound to the appID on the Device | Enables the Programmer to bind the MVPD entitlement in the token to the appID on the device it was issued to.            | Clientless API  | This aligns the Connected Device more closely to the standard Pass implementation for tokens.                             Still needs improvement to be a device-wide ID.                            |

### Device specific AuthN TTL length {#authn-ttl-length}

Enable TVE entitlement for special events that may not be resources that are in the MVPD entitlement database like normal channels.

| Priority |                Use Case               |                                                                                                                              Description                                                                                                                             | Platforms |                                                         MVPD Notes                                                         |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| High     | Set Different TTL Values Per Platform | Enables the Programmer to establish a different TTL length for  web, mobile and connected devices. Currently, Adobe Pass  authentication supports the ability to have 3 separate TTL values:                                Web (Flash)                    Mobile/HTML5                    Clientless - Connected Devices                           |           | Some MVPDs set the TTL dynamically. Adobe can override these dynamic settings if needed, using the configuration settings. |

### Special event-based applications {#special-event}

**Priority** - Low

Enable TVE entitlement for special events that may not be resources that are in the MVPD entitlement database like normal channels.

| Priority |                             Use Case                            |                                                                                                                                                                                                                                                         Description                                                                                                                                                                                                                                                        |   Platforms   |                 MVPD Notes                 |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Low      | Multiple Channels as a Proxy For an Event                       | This was done for the Olympics, where the subscriber needed to  have two different channels in their package to have access. In this  case, Adobe Pass Authentication created a new resourceID, and had  all of the MVPDs do the mapping to the specific channels on their end.  That worked fine with enough advanced notice. This was important because  most MVPDs don't support multiple resource calls.                                                                                                          | All platforms | Supported by all MVPDs with proper notice. |
| Low      | Special New Event Application, Using Existing Channel Resources | This was done for March Madness. The content provider created a  new app with a new requestorID. All MVPDs needed to add support for the  new requestorID in their system. The resourceIDs were normal channels.  Some MVPDs also needed to map the channels as valid under the new  requestor, so  more time was needed for those cases.                                                                                                                                                                                  | All platforms | Supported by all MVPDs with proper notice. |
| Low      | Existing requestorID, resourceID                                | This was done for the Masters golf weekend tournament. It was  just a small event for a couple days, and the Masters had their own  mobile app that was alright to display the content. The Programmer  planned to pay for the Adobe Pass Authentication traffic and just  use their standard requestorID and resourceID. The only trick was having  the Programmer share a mobile cert for requestorID signing with the  Masters, and have that added to their configuration as their backup cert  for that weekend. | All platforms | No impact for MVPDs                        |

### Content server integration {#content-server-integration}

**Priority**- Medium

Enabling media token validation before releasing the video stream to the client player.

| Priority  |                                                   Use Case                                                  |                                                                                                                                                              Description                                                                                                                                                             | Platforms | MVPD Notes |
|---------|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| High      | Programmer Federated Player - With Page Level Authorization                                                 | Adobe Pass Authentication APIs are done in JavaScript in the  page, and the token is passed into the player. Token can be passed to  the validation service in a couple of ways:                                 Get param on the validation service URL                    URL parameter passed in query string of the stream URL                    External Interface API                    FlashVars                           |           |            |
| Medium    | Programmer Federated Player - With Internal Player Authorization                                            | Adobe Pass Authentication APIs are done in ActionScript in  the player SWF, so the token is available to the player from the  callback.                                                                                                                                                                                         |           |            |
| High      | Syndicated Player - Hosted on MVPD Portal with Page-Level Authorization Using an iFrame to Wrap the Player  | Similar to the player with page level authorization, but with the  player page wrapper iFramed into the MVPD portal. Authentication has to  happen separately in the MVPD portal.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
