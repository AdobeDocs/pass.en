---
title: Overview For MVPDs
description: Overview For MVPDs
exl-id: b918550b-96a8-4e80-af28-0a2f63a02396
---
# An overview of MVPDs {#mvpd-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

This overview is intended for Multi-channel Video Programming Distributors (MVPDs). For additional documentation including Kickstart and Integration guides, see the Related Information section at the end of this document.

 

TV Everywhere (TVE) is the now well known industry movement that enables Pay TV subscribers to access the content that they already pay for, across multiple devices, both in and out of their homes.  For Pay TV providers, TVE creates new opportunities, both to preserve existing customer relationships and to enable new ones. Yet along with these opportunities come challenges. In the TVE landscape, Programmers provide the content, but the MVPDs hold the customer information for verifying that prospective viewers are valid subscribers. 

 

Coordinating viewer authentication and authorization with one Programmer may be straightforward, but coordinating with dozens or hundreds of different Programmers becomes increasingly complex. However, with Adobe&reg; Pass, MVPDs only need to implement a single, simple integration to get access to the entire TVE ecosystem, including Programmers such as NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu, and so on.  Adobe Pass Authentication provides an integration framework that makes determining user entitlement simple and secure.

 

Bottom line: Adobe Pass Authentication securely mediates entitlement transactions between Programmers and MVPDs, facilitating viewer access to subscription content. In other words, Adobe Pass Authentication makes it easy and quick for the right customers to access the right content.
 

With Adobe Pass Authentication,  MVPDs receive:

Easy integration with Programmers.  Deliver instant connectivity from multiple content owners with a single integration.

Enhanced customer engagement.  Support a smooth, branded experience as your customers view content across multiple platforms and devices.

Secure authentication.  Ensure that only authorized users and devices are granted access to premium content, and (optionally) limit the number of devices and concurrent streams that can connect per household account.

## FAQ {#faq}

How secure is Adobe Pass Authentication? The number one priority of the Adobe Pass Authentication architecture is to ensure that only authorized viewers are authenticated and granted access to premium content. Adobe Pass Authentication tightly binds access to viewing devices, and can help to limit streams, sessions, and / or devices for a given household.
 

Is Flash Player required? Adobe Pass Authentication for TV Everywhere is player and platform agnostic, integrating with any playback application, including Silverlight and HTML5. Additionally, Adobe Pass Authentication provides native support for devices such as phones and tablets running iOS and Android.
 

What devices does Adobe Pass Authentication support? Adobe Pass Authentication is supported by virtually any device with the HTML5 web kit for in-browser viewing experiences. Additionally, Adobe Pass Authentication is continuing to roll out native software development kits (SDKs) for various device-specific platforms, including iOS, Android&trade;, Xbox360 (Deprecated), and Adobe Air&reg; (Deprecated) applications. Most recently, Adobe Pass Authentication put out a Clientless solution, for devices that cannot render browser pages (for example, "smart" TVs, set-top boxes, and game consoles).  The ability to render browser pages is a requirement for authenticating users with MVPDs.
 

Does Adobe Pass Authentication support the emerging standards for TV Everywhere? Adobe Pass Authentication is compliant with the CableLabs OLCA (Online Content Access) specification, which provides technical requirements and architecture for the delivery of video to a Pay TV customer from online sources. Adobe participated in the joint CableLabs interopt testing project in June 2011 and passed the testing process for a Service Provider implementation. Adobe Pass Authentication is verified (complete and tested) against the OLCA specifications for authentication. The authorization component is completed, but testing verification currently awaits the release of the CableLabs testing environment. Adobe is also an active member of the OATC (Open Authentication Technical Consortium) and participates in several of the subcommittees' specification-drafting projects as part of that body.

 

What is Authentication? Authentication is the process wherein an MVPD confirms that a given user is a known customer. 

 

What is Authorization? Authorization is the process wherein an MVPD confirms that an authenticated user has a valid subscription to a given resource.

 

## Architecture {#architecture}

Adobe Pass Authentication is a hosted service that allows rapid back-end (server to server) integration based on the business rules required by both MVPDs and Programmers. This means a quick time to market for all parties, a more secure environment to prevent fraud, and a superior customer experience, with more TV content available to more people across more platforms.
 

Adobe Pass Authentication is offered via the Software as a Service (SaaS) model and enables more secure communication to take place between end users, MVPDs, and Programmers, in order to validate entitlement to content. The core components of the service include the following:

Server Side - The hosted Adobe Pass Authentication Server. This is an application server that engages in back channel (server-to-server) communication with the authentication systems of MVPDs.
Client Side:
The client-side Access Enabler - The Access Enabler is a small file that is loaded into a Programmer's web page or player application. It provides entitlement APIs to the Programmer's content viewing application, and communicates with the Adobe Pass Authentication Server.
Clientless web services (for non-web-capable devices) - RESTful web services that provide entitlement APIs for devices such as Smart TVs,  game consoles, and set-top boxes.

>[!NOTE]
>
>As an MVPD, your web services must be able to recognize requests for authentication and authorization from Adobe Pass Authentication and respond with the required data in the expected format.
>

Adobe Pass Authentication allows you to provide customers with federated identity management, also known as single sign-on (SSO) authentication and authorization. With Adobe Pass Authentication, there's no need for subscribers to log in again after their first authentication, for as long as that authentication is allowed by the MVPD to persist. (Typically, 30 days.) To accomplish this, Adobe Pass Authentication provides a common domain for authentication tokens for our customers. This authentication state information is available to all participating sites that are integrated with a given MVPD.
 

Currently, most Adobe Pass Authentication integrations with MVPDs use the SAML protocol, one of the primary authentication standards. Adobe Pass Authentication acts as a proxy Service Provider in the SAML architecture and persists the SAML authentication response as a secure token in the Adobe common domain. Adobe Pass Authentication is SAML 2.0 compliant. However, while Adobe Pass Authentication is typically used with SAML SSO solutions at this point, the Adobe Pass Authentication architecture is not bound to any specific protocol. Therefore, support for new protocols – such as one based on OAuth 2.0 or custom protocols – can be added over time.
 

Adobe works with an MVPD's technical team to configure Adobe Pass Authentication to meet the needs of any existing integrations. Integration is free of charge for MVPDs, assuming a "standard" integration and minimal support requirements (documentation and basic email support). If an MVPD requires significant support or an escalated timeline, a support fee may be charged, or the provider may want to work with a third party familiar with our solution such as Synacor.
 

Adobe Pass Authentication also supports the efficient handling of MVPD business logic, as follows:

For business logic that is self-contained and can be applied by the MVPD when a request for authorization is received, Adobe supplies the necessary data required to support the business logic enforcement when the MVPD receives an authorization request. This data can include, but is not be limited to, the unique device ID for the user making the request and the IP address of the device.

For business logic that requires user intervention and/or specific handling by the Adobe solution, Adobe can maintain some custom properties for each MVPD. These MVPD-specific configurations/policies include enablement of pre-defined workflows that can be kicked off at specific points of the top-level workflow. For details on custom property support, contact your Adobe representative.

The following diagram illustrates the relationship of the MVPD and Programmer with these Adobe Pass Authentication components:
  
![](../assets/high-level-architecture-nflows.png)

*Figure: High-level architecture and flows*

## Adobe Pass Authentication Components {#components}

The following provides an overview of some of the main components of the Adobe Pass Authentication eco-system. These include:

* [The Access Enabler / Clientless Web Services](#ae)
* [The Adobe-hosted Backend Server](#backend)
* [Tokens](#tokens)

### Access Enabler / Clientless Web Services {#ae}

The Access Enabler facilitates all authentication and authorization interactions with the user and runs locally on their system. It is the Access Enabler that handles the actual entitlement workflows with the MVPD, while the Programmer maintains responsibility for the higher-level web page or player application. 

Clientless web services are provided by Adobe Pass Authentication for devices that cannot render web pages.  For these devices, the entitlement process is initiated and content viewed on the smart device, while the authentication with an MVPD takes place on a web-capable device (PC, smart-phone, and tablet). 

The Access Enabler:

*   Initiates MVPD-specific authentication and authorization workflows.
*   Caches the successful authorization responses per Programmer resource/channel to minimize unnecessary request traffic.
*   Can be configured for predefined workflows specific to each MVPD, such as explicit device registration.
*   It is available in these forms:
    * A SWF file that the Flash Player runtime can execute
    * A JS file executed directly by the browser
    * A native Access Enabler for various platforms, including iOS, Android, and Xbox.

### Adobe-hosted Backend Server {#backend}

The Adobe Pass Authentication backend server, hosted by Adobe:

* Provisions the authentication and authorization workflows with the MVPDs that require server-to-server communication between Adobe Pass Authentication and the operator.
* Maintains the configuration for Programmer sites and applications.
* Hosts the downloadable Access Enabler component files.
* Generates authentication and authorization tokens.

### Tokens {#tokens}

The Adobe Pass Authentication entitlement solution centers on the generation of specific pieces of data that are obtained upon the successful completion of authentication/authorization workflows. These pieces of data are called tokens. They have a limited lifespan and are stored securely in platform-dependent locations. Upon expiration, tokens must be re-issued through the re-initiation of the authentication and/or authorization workflows.

There are three types of tokens that are issued during the authentication/authorization workflows. Two are "long-lived," providing continuity in the user's viewing experience. The third, a short-lived token, provides support for industry best practices for mitigating fraud through stream ripping. The time-to-live ("TTL") values for tokens are set based on agreements between MVPDs and Programmers. You decide on a TTL value that best serves your business and your customers.

**The long-lived authentication token**. Authentication success occurs once a customer uses Adobe Pass Authentication to successfully log on to their MVPD account. Adobe Pass Authentication then produces a long-lived authentication ("authN") token tied to the requesting device and (depending upon the MVPD) a globally unique identifier ("GUID") that anonymously identifies the user. 

**The long-lived authorization token**. Upon successful authorization, Adobe Pass Authentication creates a long-lived authorization ("authZ") token. This token is not portable, as it is tied to the requesting device and a specific protected resource (e.g. a channel, series, or episode). The Access Enabler uses the long-lived authZ token to create the short-lived media tokens that are used for actual viewing access. 

**The short-lived media token**. Once the user is authorized, Adobe Pass Authentication generates an authZ token, and uses that token to generate a single-use, short-lived media token that is signed by Adobe and encrypted to avoid tampering during exchange. Because the short-lived token is exposed to the embedding site through either the Access Enabler API or Clientless web services, before providing access to the protected resource, the Programmer's media server must use an Adobe Pass Authentication component, the Media Token Verifier, to validate the token.

## MVPD Integration Lifecycle {#lifecycle}

The following illustration shows the lifecycle of the integration between Adobe Pass Authentication and an MVPD.

![](../assets/mvpd-int-lifecycle.png)

*Figure: MVPD integration lifecycle*

## Entitlement Flowchart {#chart}

The following flowchart presents the overall process of confirming entitlement using Adobe Pass Authentication:

![](../assets/authn-authz-entitlmnt-flow.png)

*Figure: Process of confirming entitlement using Adobe Pass Authentication*

## Authentication Steps {#authn-steps}

The following steps present an example of the Adobe Pass Authentication authentication flow.  This is the part of the entitlement process in which a Programmer determines if the user is a valid customer of an MVPD.  In this scenario, the user is a valid subscriber to an MVPD.  The user is attempting to view protected content using a Programmer's Flash application:

1. The user browses to the Programmer's web page, which loads the Programmer's Flash application and the Adobe Pass Authentication Access Enabler components onto the user's machine. The Flash application uses Access Enabler to set the Programmer's identify with Adobe Pass Authentication, and Adobe Pass Authentication primes the Access Enabler with configuration and state data for that Programmer (the "requestor"). The Access Enabler must receive this data from the server before performing any other API calls.  Technical note: the Programmer set its identity with the Access Enabler's `setRequestor()` method.
1. When the user tries to view the Programmer's protected content, the Programmer's application presents the user with a list of MVPDs, from which the user selects a provider. 
1. The user is redirected to an Adobe Pass Authentication server, where an encrypted SAML request for the user-selected MVPD is created. This request is sent as an authentication request on behalf of the Programmer to the MVPD. Depending on the MVPD's system, the user's browser is then either redirected to the MVPD's site to log in, or a login iFrame is created in the Programmer's app.  
1. In either case (redirect or iFrame), the MVPD accepts the request and displays its login page.
1. The user logs in with the MVPD, the MVPD validates the user's status as a paying customer, and then the MVPD creates its own HTTP session.
1. When the user is validated, the MVPD creates a response (SAML & encrypted), which the MVPD sends back to Adobe Pass Authentication.
1. Adobe Pass Authentication receives the MVPD response, sees that there's an Adobe Pass Authentication HTTP session open, validates the [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) response from the MVPD, and redirects back to the Programmer's site.
1. The Programmer's site is reloaded, the Access Enabler is reloaded, and the Programmer calls setRequestor() again.  The second call to setRequestor() is necessary because the current configuration has changed–there is now a flag present that informs the Access Enabler that an AuthN token is waiting to be generated on the server.
1. The Access Enabler sees that there's a pending authentication and requests the token from the Adobe Pass Authentication server. The token is retrieved from the server by invoking the Flash Player's DRM capabilities.
1. The AuthN token is stored in the Programmer's Flash Player LSO cache; authentication is now complete, and the session is destroyed on the Adobe Pass Authentication server.

## Authorization Steps {#authz-steps}

The following steps continue on from the previous section ([Authentication Steps](#authn-steps)):

1. When the user tries to access the Programmer's protected content, the Programmer's application first checks for an AuthN token on the user's local machine or device.  If that token is not there, then the [Authentication Steps](#authn-steps) above are followed.  If the AuthN token is there, the Authorization flow proceeds with the Programmer's application initiating a call to the Access Enabler with a request to get the user's viewing rights for a specfic item of protected content.
1. The specific item of protected content is represented by a "resource identifier".  This could be a simple string or a more complex structure, but in any case the nature of the resource identifier is agreed upon ahead of time between the Programmer and the MVPD.  The Programmer's application passes the resource identifier to the Access Enabler.  The Access Enabler checks for an AuthZ token on the user's local machine or device.  If the AuthZ token is not there, the Access Enabler passes the request to the backend Adobe Pass Authentication server.
1. The Adobe Pass Authentication server communicates with the MVPDs authorization endpoint using standardized protocols.  If the MVPD's response indicates that the user is entitled to view the protected content, the Adobe Pass Authentication server creates an AuthZ token and passes it back to the Access Enabler, which stores the AuthZ token on the user's machine.
1. With an AuthZ token stored on the user's machine or device, the Programmer's application calls the Access Enabler to obtain a Media Token from the Adobe Pass Authentication server and provides that token to the Programmer's application.
1. Finally, the Programmer's application uses the Media Token Verifier component to confirm that the right user is viewing the right content, and with the Media Token in place, the user is allowed to view the protected content. 

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Pass Authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
