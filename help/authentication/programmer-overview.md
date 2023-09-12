---
title: Overview for programmers
description: Overview for programmers
exl-id: 64a12e49-0ecb-4b81-977d-60c10925bb59
---
# Overview For Programmers {#programmers-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#introduction}

This overview is intended for the content provider (Programmer) who plans to integrate Adobe&reg; Pass into their website or application. For additional documentation including Kickstart and Integration guides, see Related Information below. 

Today your viewers can get on the Internet anytime, anywhere, and request access to protected content directly from you, the Programmer. They may want to watch a one-time event, or they may be seeking viewing rights to an entire television series that you are airing. 

But before you allow access to your protected content, you have to determine whether a customer is entitled to view that content. Do they have a subscription with a Multichannel Video Programming Distributor (MVPD)? If so, does that subscription include your programming? 

Determining a viewer's entitlement is not always simple for a Programmer. The MVPDs hold the identifying data and access privileges for their customers.  Add the fact that viewers trying to access your protected content subscribe to a variety of MVPDs, each of which have different systems, and it is easy to see that determining viewer's entitlement to protected content can quickly become complicated and technically challenging:

![](assets/user-ent-by-progr.png)

*Figure: User Entitlement Determined Directly By Programmer*

Adobe Primetime authentication for TV Everywhere securely mediates these entitlement transactions between Programmers and MVPDs. Adobe Primetime authentication makes it easy, quick, and secure for Programmers to provide protected content to valid customers:

![](assets/user-ent-mediatedby-authn.png)

*Figure: User Entitlement Mediated by Adobe Primetime authentication*

Adobe Primetime authentication acts as your proxy in exchanges with participating MVPDs, so you can present your viewers with a consistent cross-site interface. Adobe Primetime authentication also allows you to provide your viewers with single-sign-on (SSO) authentication and authorization. Authentication and authorization are tracked for all participating services, so that a subscriber does not need to log in again after their first authentication on their own system.

* **Authentication** - The process of confirming with an MVPD that a given user is a known customer.
* **Authorization** - The process of confirming with an MVPD that an authenticated user has a valid subscription to a specified resource.

### How Adobe Primetime Authentication Works {#HowItWorks}

The Programmer's content-viewing application interacts with Adobe Primetime authentication using either the Access Enabler client component or the RESTful web services of the Clientless API (for non-web capable devices such as smart TVs, game consoles, set-top boxes, etc.). The Access Enabler runs on the user's system, where it facilitates all entitlement workflows.  The Access Enabler component is downloaded from its hosting site at Adobe when customers access your site and request protected content.  Adobe Primetime authentication servers host the RESTful web services used in the Clientless solution. 

Adobe Primetime authentication handles the actual entitlement workflows while providing primitives you use to:

* Set your identity. (The Programmer is the "requestor" in the Adobe Primetime authentication entitlement flow.)
* Authenticate a user with a particular MVPD.  (The MVPD is the "identity provider" or "IdP" in the Adobe Primetime authentication entitlement flow.)
* Authorize a user with the MVPD for a particular resource.
* Log out the user.

The Programmer is responsible for their upper-level web page or player application that does the following:

* Implements the user interface
* Interacts with the Access Enabler or Clientless API web services

The goal of Adobe Primetime authentication is to create a simple, modular way for both Programmers and MVPDs to handle entitlement verification. 

## Understanding Tokens {#understanding-tokens}

The Adobe Primetime authentication entitlement solution centers on the generation of specific pieces of data that are created upon the successful completion of the authentication and authorization workflows. These pieces of data are called tokens. Tokens have a limited lifespan; when they expire, tokens need to be re-issued through the re-initiation of the authentication and authorization workflows. 

For details on tokens, see the following sections:

* [Types of tokens](#token-types)
* [Token Storage](#token-storage)
* [Token Security](#token-security)
* [Token Sharing](#token-sharing)

### Types of Tokens {#token-types}

Three types of tokens are issued during the authentication and authorization workflows. The AuthN and AuthZ tokens are "long-lived", providing continuity in the user's viewing experience. The Media Token is a short-lived token that provides support for industry best practices to prevent fraud through stream ripping. Programmers specify the time-to-live (TTL) values for each type of token based on agreements made with MVPDs. Programmers decide on a TTL value that best serves your business and your customers. 

* **AuthN Token** ("Long-lived"): Upon successful authentication, Adobe Primetime authentication creates an AuthN token associated with both the requesting device and a globally unique identifier (GUID).
    * Adobe Primetime authentication sends the AuthN token to the Access Enabler, which caches it securely on the client's system.  While the AuthN token is there and unexpired, it is available to all applications that use Adobe Primetime authentication. The Access Enabler uses the AuthN token for the authorization flow.
    * At any given moment only one AuthN token is cached. Whenever a new AuthN token is issued and an old one already exists, Adobe Primetime authentication overwrites the cached token.
* **AuthZ Token** ("Long-lived"): Upon successful authorization, Adobe Primetime authentication creates an AuthZ token associated with the requesting device and a specific protected resource.  The protected resource is identified by a unique resource ID.
    * Adobe Primetime authentication sends the AuthZ token to the Access Enabler, which caches it securely on the local system. The Access Enabler then uses the AuthZ token to create the short-lived Media token that is used for actual viewing access.
    * At any given time only one AuthZ token per resource is cached. Adobe Primetime authentication can cache multiple AuthZ tokens, as long as they are associated with different resources. Whenever a new AuthZ token is issued and an old one already exists for the same resource, Adobe Primetime authentication overwrites the cached token.
* **Media Token** ("Short-Lived"): The Access Enabler uses the AuthZ token to generate a short-lived (default: 7 minutes) Media token. This is the point at which a successful play request is considered to have occurred.
    * Before providing access to the protected resource, your media server must use an Adobe Primetime authentication component, the Media Token Verifier, to validate the Media token.
    * Because the Media token is not bound to the device, its life-span is significantly shorter (default: 7 minutes) than that of the long-lived AuthN and AuthZ tokens.
    * The short-lived media token is restricted to one-time use and is never cached. It is retrieved from the Adobe Primetime authentication server every time an authorization API is called.

### Token Storage {#token-storage}

The Access Enabler stores long-lived tokens (AuthN and AuthZ) in locations specific to its environment:

* **Flash 10.1** (or higher): The long-lived tokens are stored as Local Shared Objects.
* **HTML5**: The long-lived tokens are kept securely in the HTML5 browser's local store.
* **iOS**: The long-lived tokens are stored on a persistent pasteboard, where they can be accessed by other Adobe Primetime authentication client applications.
* **Android**: The long-lived tokens are stored in a shared database file, where they can be accessed by other Adobe Primetime authentication client applications.
* **Clientless API devices**: Tokens are stored on the Primetime authentication servers.

### Token Security {#token-security}

The Adobe Primetime authentication Server digitally signs all long-lived tokens using the device ID (derived from device's hardware characteristics). The digital signature differs in how it is generated, protected, and validated depending upon the environment:

* **Flash 10.1** (or higher) - The device ID relies on the device credential, a unique certificate issued from the Adobe Individualization server. This security is equivalent to FAXS DRM technology. This server-side validation compares the unique device ID in the token with the device credential (securely communicated from Flash Player to Adobe Primetime authentication). The device credential also identifies the FAXS client version and the Flash Player (or AIR) version to which it was issued. The device binding is stronger than with HTML5, so the time-to-live (TTL) for tokens is typically longer with Flash.
* **HTML5** - The device is individualized on the client side. It uses characteristics available through JavaScript to produce a pseudo-device ID that includes browser and OS versions, an IP address, and a browser cookie GUID (globally unique identifier). This token device ID is compared to the current pseudo-device ID for the device. Because the IP address can change during normal use, even in the same session, Adobe Primetime authentication stores HTML5 tokens in two locations: localStorage and sessionStorage. If the IP changes and the sessionStorage token is otherwise still valid, the session is maintained. With HTML5, the device binding is not as strong, so the TTL for tokens is typically shorter than for Flash.
* **Native Clients** (iOS and Android) - The long-lived tokens hold native device ID individualization info and thus are bound to the requesting device. The authentication and authorization requests are sent over HTTPS, and the device ID information is digitally signed by the Access Enabler library before sending it to the backend servers. On the server side, the device ID info is validated against its associated digital signature.
* **Clientless API Clients** - The Clientless API solution has its set of security protocols that involve digitally signing all API calls. Tokens generated during the entitlement flows are securely stored on the Adobe Primetime authentication servers.

Adobe Primetime authentication validates each long-lived token to ensure that the device accessing the content is the same as the one that issued the token. For all tokens, a client-side validation ensures that the digital signature is intact, and that the integrity of the token is preserved. When device ID validation fails, the authentication session is invalidated, and the user is prompted to log in again, which resets the tokens. 

### Token Sharing {#token-sharing}

Applications on different platforms do not share tokens. There are a number of reasons for this, including the following:

* As described in [Token Storage](#token-storage), the method of storing tokens varies between platforms (for example, Local Shared Objects for Flash, WebStorage for JavaScript). 
* The degree of token security differs between platforms. For example, Flash tokens are strongly bound to a device using FAXS. Tokens in a pure JavaScript environment do not have the same level of DRM support as in Flash.  Sharing JS tokens with Flash applications would increase the possibility of less secure tokens exploiting a more secure environment.

## Programmer Integration Lifecycle {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Figure: Integrating Authentication with programmer's website and application*


## Logical Flows {#logical-flows}

### Entitlement Flowchart {#chart}

The following flowchart presents the overall process of confirming entitlement (using the Adobe Primetime authentication Access Enabler client component):

![](assets/ent-flowchart.png)

*Figure: Process of confirming entitlement*

### Authentication Steps {#authn-steps}

The following steps present an example of the Adobe Primetime authentication authentication flow.  This is the part of the entitlement process in which a Programmer determines if the user is a valid customer of an MVPD.  In this scenario, the user is a valid subscriber to an MVPD.  The user is attempting to view protected content using a Programmer's Flash application:

1. The user browses to the Programmer's web page, which loads the Programmer's Flash application and the Adobe Primetime authentication Access Enabler components onto the user's machine. The Flash application uses Access Enabler to set the Programmer's identify with Adobe Primetime authentication, and Adobe Primetime authentication primes the Access Enabler with configuration and state data for that Programmer (the "requestor"). The Access Enabler must receive this data from the server before performing any other API calls. Technical note: the Programmer set its identity with the Access Enabler's `setRequestor()` method; for details, see the [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md).
1. When the user tries to view the Programmer's protected content, the Programmer's application presents the user with a list of MVPDs, from which the user selects a provider. 
1. The user is redirected to an Adobe Primetime authentication server, where an encrypted [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) request for the user-selected MVPD is created. This request is sent as an authentication request on behalf of the Programmer to the MVPD. Depending on the MVPD's system, the user's browser is then either redirected to the MVPD's site to log in, or a login iFrame is created in the Programmer's app.  
1. In either case (redirect or iFrame), the MVPD accepts the request and displays its login page.
1. The user logs in with the MVPD, the MVPD validates the user's status as a paying customer, and then the MVPD creates its own HTTP session.
1. When the user is validated, the MVPD creates a response (SAML & encrypted), which the MVPD sends back to Adobe Primetime authentication.
1. Adobe Primetime authentication receives the MVPD response, sees that there's an Adobe Primetime authentication HTTP session open, validates the SAML response from the MVPD, and redirects back to the Programmer's site.
1. The Programmer's site is reloaded, the Access Enabler is reloaded, and the Programmer calls setRequestor() again.  The second call to setRequestor() is necessary because the current configuration has changed-there is now a flag present that informs the Access Enabler that an AuthN token is waiting to be generated on the server.
1. The Access Enabler sees that there's a pending authentication and requests the token from the Adobe Primetime authentication server. The token is retrieved from the server by invoking the Flash Player's DRM capabilities.
1. The AuthN token is stored in the Programmer's Flash Player LSO cache; authentication is now complete, and the session is destroyed on the Adobe Primetime authentication server.

### Authorization Steps {#authz-steps}

The following steps continue on from the [Authentication Steps](#authn-steps):

1. When the user tries to access the Programmer's protected content, the Programmer's application first checks for an AuthN token on the user's local machine or device.  If that token is not there, then the [Authentication Steps](#authn-steps) above are followed.  If the AuthN token is there, the Authorization flow proceeds with the Programmer's application initiating a call to the Access Enabler with a request to get the user's viewing rights for a specfic item of protected content.
1. The specific item of protected content is represented by a "resource identifier".  This could be a simple string or a more complex structure, but in any case the nature of the resource identifier is agreed upon ahead of time between the Programmer and the MVPD.  The Programmer's application passes the resource identifier to the Access Enabler.  The Access Enabler checks for an AuthZ token on the user's local machine or device.  If the AuthZ token is not there, the Access Enabler passes the request to the backend Adobe Primetime authentication server.
1. The Adobe Primetime authentication server communicates with the MVPDs authorization endpoint using standardized protocols.  If the MVPD's response indicates that the user is entitled to view the protected content, the Adobe Primetime authentication server creates an AuthZ token and passes it back to the Access Enabler, which stores the AuthZ token on the user's machine.
1. With an AuthZ token stored on the user's machine or device, the Programmer's application calls the Access Enabler to obtain a Media Token from the Adobe Primetime authentication server and provides that token to the Programmer's application.
1. Finally, the Programmer's application uses the Media Token Verifier component to confirm that the right user is viewing the right content, and with the Media Token in place, the user is allowed to view the protected content. 


## Registration and Initialization {#reg-and-init}

The first step in working with Adobe Primetime authentication is to register with Adobe, or with an Adobe Primetime authentication-authorized partner. 

When you register, you provide a list of the domains from which you will communicate with Adobe Primetime authentication. For example, the Turner Broadcasting System domains include tbs.com and tnt.tv as Adobe Primetime authentication-registered domains. Each of these content sites is given access to Adobe Primetime authentication, and is assigned its own Requestor ID (for example, "TBS", and "TNT"). If you decide to add additional sites, you must inform Adobe of the additional domain names to get them placed on the list of allowed domains and be given additional Requestor IDs.
    
>[!WARNING]
>
>While you are testing your integration, make sure that your test server is on a registered domain that you intend to use in production. Requests, even test requests, coming from non-whitelisted domains are ignored. For example, if you requested domain.com to be used in production, make sure you are deploying your test integration under domain.com, test.domain.com, and staging.domain.com.
>
>Requests that contain username and / or password in the URL are ignored even if domains are whitelisted. Example: `//username@registered-domain/`

The Requestor ID uniquely identifies the Programmer's client in all communications with Adobe Primetime authentication's Access Enabler client component. All Adobe Primetime authentication static data associated with the Programmer is keyed to this ID.

>[!TIP]
>
>In addition to your Requestor ID, when you register you also receive functional URLs for the Access Enabler client component and Media Token Verifier.

## Integration Steps {#integration-steps}

>[!TIP]
>
>If you are using Adobe's Open Source Media Framework ("OSMF") for your media player development, the quickest way to use Adobe Primetime authentication is to integrate the OSMF Plugin *(Deprecated)* into your player's code. 
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Requestor Setup](#requestor)
1. [Handling Authentication and Authorization](#authn-authz)
1. [Supporting Single Logout](#ssl)

### 1. Requestor Setup {#requestor}

#### 1a. Registering With Adobe

Your first step is to register with Adobe, or with an Adobe Primetime authentication authorized partner.  When you register you are issued one or more globally unique identifiers (GUIDs). Each GUID you are issued is associated with a domain from which access is allowed to Adobe Primetime authentication. You pass a GUID (called the requestor ID) for the requesting domain to register your identity for each session in which you interact with the Access Enabler. For details, see [Registration and Initialization](#reg-and-init) in the Programmer Integration Guide.  

#### 1b. Initial Access Enabler Integration

The next step is to integrate the Access Enabler into your existing media player app or web page:

*   You can embed the Flash version, `AccessEnabler.swf`, in a Flash-based video player, or you can embed it directly in your web page's HTML. You can communicate with the Access Enabler SWF in either ActionScript or JavaScript. The base API is ActionScript, but if you prefer to work with JavaScript, a complete wrapper library is available for inclusion on your pages.
*   For non-Flash environments, you can:
    * Use the HTML5/JavaScript version, AccessEnabler.js, and communicate with it through the JavaScript API
    * Use the AIR Native Extension for Adobe Primetime authentication to combine native code with built-in ActionScript classes
    * Use one of the native client versions of the Access Enabler library (iOS or Android)

### 2. Handling Authentication and Authorization {#authn-authz}

#### 2a. Communicating with the Access Enabler

Communication between the Access Enabler and your web page or player app is asynchronous. Your application calls Access Enabler methods, and the Access Enabler responds via callbacks that you register with the Access Enabler library.

* When your application makes an authorization request, the Access Enabler automatically initiates an authentication request, if a valid AuthN token is not already on the local system. When authentication succeeds, the user's AuthN token is stored locally, so that they do not need to log in again. If they have successfully authenticated through Adobe Primetime authentication in any other context (for example, through the MVPD website or with a different Programmer), the Access Enabler has access to the local AuthN token and an additional authentication is not needed.
* When a user attempts to access your protected content, you send an authorization request to the Access Enabler. After verifying (or initiating) authentication, the Access Enabler contacts the MVPD (via the Adobe Primetime authentication server) to determine whether the customer is entitled to view the protected content. Your application only needs to send the request to the Access Enabler, and then handle the response (authorization success or failure). If authorization succeeds, an AuthZ token is stored on the client system.  Finally, your application receives a short-lived Media token for use in your own authorization procedure.

>[!NOTE]
>
>*   Authentication occurs as a SAML exchange, between Adobe Primetime authentication as the Service Provider (SP) and the MVPD as the Identity Provider (IdP).
>
>*   Authorization uses a back-channel (server-to-server) web-service exchange between Adobe Primetime authentication (the SP) and an MVPD (the IdP).


#### 2b. Providing An Entitlement User Interface {#entitlement-ui}

You provide your own UI for user access to your content. Some elements, such as the actual login process, are provided by the MVPD, and some elements are optionally available as part of Adobe Primetime authentication. At minimum, you do the following:

* **Implement an MVPD selection interface that allows a new user to identify their MVPD and log in for the first time**. For development, the Access Enabler provides a basic user interface that gives the customer a choice of MVPDs and initiates the login process. For production, you must implement your own MVPD Selector dialog. Some MVPDs redirect to their own site for login, and some require their login pages to be displayed within an iFrame. You must implement a callback that creates this iFrame to handle the cases where the user's MVPD displays their login page in an iFrame.
* **Identify protected content**. Protected content requires authorization to access. Your interface should indicate which content is protected, and which content has been authorized.  Authorization status is often indicated with "unlocked" and "locked" icons.
* **Show that a user is authenticated**. You should indicate a user's authentication status as part of whatever means you use to identify protected content. You can query the Access Enabler to determine whether the customer has already been authenticated.

#### 2c. Integrating the Media Token Verifier {#int-media-token-ver}

You must integrate the Adobe Primetime authentication Media Token Verifier component into your media server.  This is so your existing token verifier can recognize the short-lived Media tokens provided from Adobe Primetime authentication with a successful authorization. The Media Token Verifier validates the Media tokens as the last security step before you provide the user access to protected content. You receive the location from which to download the Media Token Verifier when you register with Adobe.

### 3. Supporting Single Logout {#ssl}

In most cases, your media player is responsible for handling user logouts via a simple Access Enabler API. When you call logout(), the Access Enabler does the following:

* Logs out the current user
* Clears all authentication and authorization information for the logged out user
* Deletes all AuthN and AuthZ tokens from the user's local system

If the user leaves their machine idle long enough for their tokens to expire, the user can still return to the session and successfully initiate logout. Adobe Primetime authentication ensures that all tokens are deleted, and notifies the MVPD to delete their session as well. 

When the logout is initiated from a site that isn't integrated with Adobe Primetime authentication, the MVPD can invoke the Adobe Primetime authentication Single Logout service through a browser redirect.

## Understanding User IDs {#user-ids}

Conceptually, each user who initiates an entitlement flow is associated with a single, unique user ID.  However, through the course of an entitlement flow, that one user ID can be presented in different ways, depending upon which API you obtain the ID from. 

The sessionGUID in the Short Media Token is the secure form of the UserID, which is available via the sendTrackingData() call.   In all current integrations, this is a persistent GUID for the user across time and devices, but the source of the GUID starts with the UserID in the SAML response from the MVPD.   However, some MVPDs could change their mind in the future, and start sending a transient GUID.  If a Programmer wants to ensure that the MVPD source UserID in the AuthN response is persistent, they should arrange for that in their agreements with MVPDs.  

Here are the different ways the User ID is represented in the Adobe Primetime authentication APIs:

* `sendTrackingData()` GUID property - This is the Adobe hashed version of the MVPD UserID.  It is hashed so this User ID is not trackable back to the source from the MVPD.   This ID is unique and typically persistent, but it can't be shared with the MVPD to compare specific usage behavior with what MVPDs have on their side.   It is not digitally signed, so not unspoofable for fraud prevention, but it is good enough for analytics.  This form of the User ID is provided client-side on all of the events that Adobe Primetime authentication generates in the AuthN/AuthZ flow. 
* Short Media Token's `sessionGUID` property - This is the same as the UserID via `sendTrackingData()`, however, this one is digitally signed to protect its integrity.  That makes this value good enough for fraud tracking of concurrent usage. It is intended to be processed on the server side after using our validator library, and can be analyzed for fraud patterns before releasing the video stream to the client.  Doing any of these tasks is up to the Programmer.  
* `getMetadata() userID `property - This property will allow Adobe to expose the actual source MVPD UserID to the Programmer. It will be encrypted with the public key from the certificate we have from the Programmer, so that it is not exposed in the clear to the client. This gives the Programmer the actual UserID from the MVPD, so it is something that can be used for account linking or fraud investigation directly with the MVPD.

**In conclusion**

* The MVPD User ID is a generally, though not guaranteed, persistent unique ID that is **generated from the MVPDs and passed to Adobe on successful authentication**. It is generally consistent across all networks with some exceptions.
* The MVPD User ID does not contain PII and it is NOT an account number. It does not need to be exposed in an encrypted form since we have validated with all the MVPDs that no PII is being sent.   


How you use the user ID depends on the use case:

* If you need it for tracking/analytics, the most practical place is to get it from `sendTrackingData()`.
* If you need it on the server-side for stream release, fraud, or operational data, you can get it from the Media Token Validator.
* If you need it for account linking and deeper fraud, check with your Adobe contact for availability.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->
