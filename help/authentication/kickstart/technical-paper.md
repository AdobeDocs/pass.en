---
title: About Adobe Pass Authentication and TV Everywhere
description: About Adobe Pass Authentication and TV Everywhere
exl-id: 5edeaccb-f9fa-4395-83b4-706c518d5a03
---
# About Adobe Pass Authentication and TV Everywhere {#about-auth-tve}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## About TV Everywhere {#about-tve}

Today's television viewers can go online at any time or place, and they expect their ability to access Pay TV content to be right there with them. In addition, audiences are viewing content using an ever-increasing range of Internet­‐capable devices, including:

* Laptops
* Tablets
* Smartphones
* Web Sites
* Federated Apps
* Game Consoles
* Set-top Boxes
* Smart TVs

TV Everywhere is the industry movement that supports the ability of Pay TV subscribers to access the same content that they are already paying for, across multiple devices, both in and out of their homes. While the bulk of television viewing is still occurring on conventional, linear TV, the growth in consumption is in time-­shifted content, online video, and alternative screens. As a result, the video distribution market today is in a state of disruption, and TV Everywhere has emerged as the solution that aligns the interests of Programmers, Pay TV providers, and Pay TV subscribers.
 

The technical goal of TV Everywhere is to enable Pay TV customers to access content that they already subscribe to on all of their devices and platforms.
 

The business goals of TV Everywhere are to:

* **Preserve existing customer relationships and enable new ones**
* Allow Programmers and content owners to reach the widest audience and capture more value from premium content
* Extend brands through direct online interaction with viewers

## TV Everywhere Challenges {#tve-challenges}

Along with the opportunities of TV Everywhere come challenges. At the heart of these is entitlement. Before a viewer accesses subscription content, someone has to determine whether they are entitled to that access.

Does the user have a subscription with a Pay TV provider? If so, does that subscription include the content that is being requested? Entitlement is especially difficult for Programmers and content owners to directly determine, because it is the Pay TV operators that have the identifying data for their customers, as well as their customers' access privileges.
 

Beyond entitlement are a host of related technical and integration challenges, including:

* Developing and enacting a comprehensive multi-­device strategy
* Coordinating the myriad relationships between Programmers and Pay TV providers
* Preventing fraudulent access, or abuse of terms of service
* Providing a consistent and frustration-free authentication experience for users across websites and apps
* Maintaining a quick time to market to keep up with affiliate deals
* Managing costs associated with multiple integrations

These challenges make performing and maintaining complex, direct integrations between Programmers and the authentication systems of multiple Pay TV providers highly resource intensive, requiring time and technical sophistication.
 

The solution? **Adobe&reg; Pass Authentication**.

## Introduction to Adobe Pass Authentication {#authentication-intro}

With Adobe Pass Authentication, Programmers and Pay TV providers only need to do a simple integration, using Adobe Pass Authentication APIs, to get access to the whole ecosystem, including:

* Programmers such as Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, and Hulu

* All of the top Pay TV providers in the US, comprising over 90% of all US Pay TV households

In addition, Adobe Pass Authentication provides the framework that makes user authentication and authorization simple and secure.

![](../assets/programmers-connect-authn.png)

*Figure 1: Just some of the Programmers and Pay TV providers who connect through Adobe Pass Authentication...*

Adobe Pass securely mediates entitlement transactions between Programmers and Pay TV providers, facilitating viewer access to subscription content. Or, in other words...

**Adobe Pass Authentication makes it easy and quick for the right customers to access the right content.** 

**Who is Adobe Pass Authentication for?**

*   **Programmers** who want to easily integrate with Pay TV providers (also known as "MVPDs" or "Multichannel Video Programming Distributors"), reaching the widest audience, for optimal revenue. Using Adobe Pass Authentication, Programmers can authenticate viewers across all major providers, independent of client platform.

*   **Pay TV providers/MVPDs** who seek painless connectivity with multiple Programmers and higher customer satisfaction by facilitating access to subscription content online.

*   **Pay TV customers** who want easy access to content they already subscribe to, wherever they are, at no additional fee. Single sign‐on provides secure viewer authentication across the web or across mobile apps, without requiring client downloads or repeated log-ins, as well as a good user experience.

For **Programmers**, Adobe Pass Authentication provides:

* Easy integration and instant connectivity with top Pay TV providers, without the pain of multiple, direct integrations
* Optimization of both subscription (licensing) and advertising revenue by supporting the widest possible audiences for content
* Secure authentication, with access to premium content granted only to authorized users/devices
* An open and flexible framework that is both player and DRM platform agnostic; playback can occur on a wide array of platforms, including iOS, Android, Windows 8, game consoles, set-top boxes, and more.  
* Compatibility with any DRM technology, such as Adobe Flash Access&reg; or Play Ready&reg;.
* Support for Single-Sign-On (SSO) authentication and authorization, so that subscribers don't need to log in again after their first authentication on their own system.


For **Pay TV providers/MVPDs**, Adobe Pass Authentication provides:

* Easy integration with content owners, delivering instant connectivity with multiple Programmers using a single integration
* Enhanced customer engagement by supporting a smooth, branded experience as they view content across multiple platforms and devices
* Secure authentication that ensures that only authorized users/devices are granted access to premium content, and (optionally) limits the number of devices and concurrent streams that can connect per household account.
 

For **Pay TV customers**, Adobe Pass Authentication provides:

* **TV Everywhere!**
 
The rest of this  paper provides a technical introduction to Adobe Pass Authentication.  While much of the following focuses on Programmer integration, there is both general and specific information that applies to Pay TV providers, as well. This document also highlights the security and integrity of how Adobe Pass Authentication functions as a solution for TV Everywhere. For further details beyond this  paper, contact your Adobe representative or fill out the Request for Information form [here](https://www.adobe.com/).

## Architectural Building Blocks {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) The following discusses the central entitlement transactions of authentication and authorization. Authentication is the process of confirming with a Pay TV provider that a given user is a known customer. Authorization is the process wherein a Pay TV provider confirms that an authenticated user has a valid subscription to a given resource.
Adobe Pass Authentication consists of the following basic components:

*   Client Component (one of the following):

    * The Access Enabler - A platform-specific library; provides easy-to-use APIs and code samples for implementing the entitlement flows
    * The Clientless API - RESTful web services; provides entitlement flow endpoints for platforms without webpage rendering abilities (such as game consoles, set-top boxes, etc.)

*   Adobe-hosted Backend Servers
*   The Media Token Verifier
*   A Secure, Central Medium of Exchange (Tokens)

At a basic level, Adobe Pass Authentication consists of three components (the Access Enabler, Adobe-hosted backend servers, and the Media Token Verifier) and a central item of exchange (tokens).

### Client Components {#client-components}

* Access Enabler
* Clientless API

#### Access Enabler {#access-enabler}

On fully supported platforms (including the Web, iOS, Android, Windows 8), Programmers interact with Adobe Pass Authentication via the Access Enabler client component. This component facilitates all authentication and authorization interactions with the customer.  The Access Enabler runs locally on their system. When a user accesses a Programmer site or application and requests content, the Adobe-hosted/maintained Access Enabler component is silently loaded in the background. 

The Access Enabler handles the actual entitlement workflows, while the Programmer maintains responsibility for the higher-level web page or player application that implements the user interface and interacts with the Access Enabler. These interactions are via an asynchronous system of functions and callbacks, defined by the Access Enabler API.

These are the basic entitlement flows, easily implemented using the Access Enabler API:

* Setting the requestor (Programmer) identity
* Checking/obtaining user authentication against a particular Pay TV operator (the "Identity Provider")
* Checking/obtaining user authorization for a particular resource
* Logging out the user

The Access Enabler also provides the following services:

* It validates queries from the Programmer, including the registration status of specific clients, their domains, and their resources/channels.
* It supplies the data that creates the list of Pay TV operators from which the user selects their provider. This list is also validated and defined as appropriate for the Programmer from which the request originates.
* It initiates Pay TV operator-specific authentication and authorization workflows.
* It caches the successful authorization responses per Programmer resource/channel to minimize unnecessary request traffic.
* It can be configured for predefined workflows specific to each Pay TV operator, such as explicit device registration.

Depending on your website or player application, the Access Enabler can take the following forms:

* A SWF file that the Flash Player runtime can execute
* A JS file executed directly by the browser
* A native Access Enabler for supported platforms (including iOS, Android, and Windows 8)

#### Clientless API {#clientless-api}

The Clientless API approach is for "smart devices" (game consoles, set-top boxes, and Smart TVs) that do not support web browsers (required for authentication with MVPDs).  In the clientless approach, smart device apps communicate directly with Adobe Pass Authentication through RESTful web services APIs for everything except authentication, which is performed on a second screen (browser) app. In other words, the Access Enabler client-side library is not used. Instead, developers of smart device apps directly consume the Adobe Pass Authentication web services APIs to implement the entitlement flows.

### Adobe-hosted Backend Servers {#adobe-backend-servers}

The Adobe Pass Authentication backend servers, hosted by Adobe:

* Provision the authentication and authorization workflows with the Pay TV providers that require server-to-server communication between Adobe Pass Authentication and the operator.
* Maintain the configuration for Programmer sites and applications.
* Host the downloadable Access Enabler component files.
* Provide the RESTful web service endpoints for the Clientless API integration.
* Generate (and in some cases, store) authentication and authorization tokens.

### Tokens and the Media Token Verifier {#tokens-media-token-verifier}

The Adobe Pass Authentication entitlement solution centers on the generation of specific pieces of data that are obtained upon the successful completion of authentication/authorization workflows. These pieces of data are called tokens. They have a limited lifespan and are stored securely, either in platform-dependent locations on the client, or on Adobe servers in the case of the Clientless API solution. Upon expiration, tokens must be re-issued through the re-initiation of the authentication and/or authorization workflows.

There are three types of tokens that Adobe Pass Authentication issues during the authentication/authorization workflows. Two are "long-lived," providing continuity in the user's viewing experience. The third, a short-lived token, provides support for industry best practices for mitigating fraud (where fraud includes exploits such as stream ripping, for example). The time-to-live ("TTL") values are set based on agreements between Programmers and Pay TV providers, who agree on a value that best serves everyone involved.

#### (Long-Lived) Authentication Token {#long-lived-auth-token}

Authentication success occurs once a customer uses Adobe Pass Authentication to successfully log in to their Pay TV account. Adobe Pass Authentication then produces a long-lived authentication (AuthN) token tied to the requesting device and (depending upon the Pay TV provider) a globally unique identifier ("GUID") that anonymously identifies the user.

* Adobe Pass Authentication stores the AuthN token securely in a location where it is available to all applications that use Adobe Pass Authentication. For Access Enabler integrations, tokens are stored securely on the client side.  Adobe Pass Authentication uses the AuthN token to make subsequent authorization queries on the user's behalf.
* At any given moment only one AuthN token is stored. Whenever a new AuthN token is issued and an old one already exists, the new token overwrites the existing stored value.

#### (Long-Lived) Authorization Token {#long-lived-authriz-token}

Upon successful authorization, Adobe Pass Authentication creates a long-lived authorization ("AuthZ") token. This token is not portable, as it is tied to the requesting device and a specific protected resource (for example, a channel, series, or episode).

* Adobe Pass Authentication stores the AuthZ token securely, along with other authorization tokens for other resources.  Again, as with the AuthN tokens, on platforms using the Access Enabler the token is stored locally on the client; on platforms using the Clientless API, tokens are stored on the Adobe Pass Authentication servers.
* The time-to-live (TTL) of the long-lived AuthZ token is typically defined in the range of days to weeks, depending on the specific agreement between the Pay TV provider and the Programmer.
* At any given time only one AuthZ token per resource is stored. There can be multiple authorization tokens stored, as long as they are associated with different resources. Whenever a new authorization token is issued and an old one already exists for the same resource, the new token overwrites the existing cached value.
* Adobe Pass Authentication uses the long-lived AuthZ token to create the short-lived media tokens that are used for actual viewing access.

#### Short-Lived Media Token {#short-lived-media-token}

Once Adobe Pass Authentication generates the AuthZ token, it uses that token to generate a single-use, short-lived media token that is signed by Adobe and encrypted to avoid tampering during exchange:

* The TTL of the short-lived token (default: 5 mins) is set to allow for clock-synchronization issues between the server generating the token and the server validating the token.
* The short-lived token is exposed to the embedding site before providing access to the protected resource, so the Programmer must validate the token, using the Media Token Verifier for Access Enabler integrations, or the Token Verifier Service in the case of Clientless API integrations.

#### Media Token Verifier {#media-token-verifier}

Programmers are responsible for integrating the Media Token Verifier Library into their existing application server, so that the Verifier can perform the final user validations before a video stream is actually started. The Media Token Verifier library defines:

* A token-verification API that retrieves information from the token such as whether it is valid, the time the token was issued, and other relevant data
* The Adobe public key used to verify that the token does indeed come from Adobe
* A reference implementation showing how to use the Verifier API and how to use the Adobe public key contained in the library to verify its origin
  
![](../assets/high-level-architecture-nflows.png)

*Figure 2: High-level architecture of the Adobe Pass Authentication ecosystem in an Access Enabler integration*

## Integrate with Adobe Pass Authentication {#integrate-auth}

Whether you are a Pay TV provider or Programmer, the process of integrating with Adobe Pass Authentication requires some amount of your active participation. Each of these processes is described below.

### The Pay TV Provider Process

The Pay TV provider's primary responsibility with Adobe Pass Authentication is to validate that a requesting user is indeed a known subscriber who is entitled to access the Programmer's content. At a high
level, the Adobe Pass Authentication process for integrating with a new Pay TV provider requires the following steps:

1. The provider signs the Adobe Pass Authentication Non-Disclosure Agreement (NDA).
1. The provider supplies Adobe with specifications for their authentication and authorization system. For the simplest integration, is recommended that Pay TV operators have a SAML-based identity provider (IdP) for authentication and the ability to communicate via the SOAP access protocol for authorization.
1. The provider establishes connectivity between their servers and the Adobe Pass Authentication servers. This includes supplying endpoints,and listing IPs.
1. Pre-Qualification Release and QE.
1. Production Release and QE.
  
While Adobe Pass Authentication may replace existing integrations for Programmers, this is typically not required for Pay TV providers. Adobe works with the provider's technical team to configure Adobe Pass Authentication to meet the needs of any existing integrations. Integration is free of charge for Pay TV providers, assuming a "standard" integration and minimal support requirements (documentation and basic email support). If a provider requires significant support or an escalated timeline, a support fee may be charged or the provider may want to work with a third party familiar with our solution such as Synacor.
 

Adobe Pass Authentication also supports the efficient handling of Pay TV provider business logic, as follows:

* For business logic that is self-contained and can be applied by the operator when a request for authorization is received, Adobe supplies the necessary data required to support the business logic enforcement when the operator receives an authorization request. This data can include, but may not be limited to, the unique device ID for the user making the request and the IP address of the device.
* For business logic that requires user intervention and/or specific handling by the Adobe solution, Adobe can maintain some custom properties for each Pay TV provider. These operator-specific configurations/policies include enablement of pre-defined workflows that can be kicked off at specific points of the top-level workflow. For details on custom property support, contact your Adobe representative.

Adobe also offers fraud-limiting services. Contact your Adobe representative for details.

### The Programmer Process {#programmer-process}

To successfully integrate Adobe Pass Authentication, Programmers must set up their media player application or web page to work with Adobe Pass Authentication in handling the core entitlement processes: authentication, authorization, and logout.
 

Prior to beginning an integration with Adobe Pass Authentication, Programmers should have:

* An existing online video platform, including a media player, either as part of a website or as a standalone application
* A content management system
* A delivery mechanism, which may or may not include a third-party content delivery network (CDN)

Programmers should expect to perform some integration tasks as part of providing TV Everywhere services with Adobe Pass Authentication. These tasks include:

* Integrating Adobe Pass Authentication's Access Enabler library into your web page or media player, or implementing integration using the Clientless approach for "smart devices" that aren't web capable
* Server-side work to integrate the Adobe Pass Authentication token verifier component into your video streaming workflow
* Creating a UI for the access workflow into your website or app (some elements of this, such as the actual login process, are provided by the Pay TV operator, and some elements are optionally available as part of Adobe Pass Authentication)

This paper provides an overview of the Programmer process, and Adobe provides additional guidance upon formal initiation of the integration.

#### Requestor (Programmer) Setup {#requester-prog-setup}

##### Registering with Adobe {#registering}

As a first step, Programmers must register with Adobe or an Adobe-authorized partner and specify the domains that they want to use with Adobe Pass Authentication. Programmers then receive a unique requestor ID, which is supplied to Adobe Pass Authentication for each session in which the Programmer interacts with the Access Enabler.

##### Setup For Initial Access Enabler Integration {#access-enabler-int-setup}

Prior to any customers requesting access to content, Programmers must integrate the Adobe Pass Authentication client component – the Access Enabler – into their existing media player app or web page. There are various options as to how to do this:

*   You can embed the Flash version, AccessEnabler.swf, in a Flash-based video player on a web page, or directly in HTML. You can communicate with the SWF in ActionScript or JavaScript. The base API is ActionScript, but a complete JavaScript wrapper library is available.
*   For non-Flash devices, you can:
    * Use the HTML5/JavaScript version, AccessEnabler.js, and communicate with it through the JavaScript API, or
    * Use a native Access Enabler library, such as for iOS, Android, or Windows 8

##### Setup for Initial Clientless API Integration {#clientless-api-int-setup}

Prior to any customers requesting access to content, Programmers must implement the RESTful web services calls using the Clientless API into their media player app, as well as set up a "second-screen" application to handle the user's log in to their Pay TV Provider over the web.

#### Handling Authentication and Authorization {#auth-authr-handling}

When a customer requests a protected resource from a Programmer for the first time, the Programmer presents the customer with a list of Pay TV providers from which to choose. When the provider is selected, the user is redirected to that operator for initial user authentication. Once authentication succeeds, Adobe Pass Authentication communicates with the selected Pay TV provider to authorize access to the specified resource. Details on these processes follow.
  
![](../assets/providr-selection-ui.png)


*Figure 3: Example provider-selection UI*  

>[!NOTE]
>
>* Authentication occurs as a SAML exchange between Adobe Pass Authentication as the Service Provider (or "SP") and a Pay TV provider as the Identity Provider (or "IdP").
>* Authorization uses a back-channel (server-to-server) web-service exchange between Adobe Pass Authentication (the SP) and a Pay TV provider (the IdP).


##### Programmer Communication using the Access Enabler

The two-way communication channel between the Access Enabler and the Programmer's web page or player app follows a fully asynchronous pattern. The Programmer sends messages to the Access Enabler through the methods exposed by the Access Enabler API. The Access Enabler responds via callbacks that are registered with the Access Enabler library.

* Any request for authorization automatically requests authentication first, if an authentication token is not found on the local system. When authentication succeeds, the customer's token is stored locally, so that they do not need to log in again for a given period of time. If they have successfully authenticated through the Adobe Pass Authentication entitlement solution in any other context (e.g., through the Pay TV provider's website or a different Programmer), the Access Enabler has access to the local token and does not require an additional authentication to be performed.
* When a customer requests a specific resource, the Programmer requests authorization from the Pay TV provider via the Access Enabler. After verifying (or initiating) authentication, the Access Enabler contacts the Pay TV provider (through Adobe Pass Authentication) to determine whether the customer is entitled to view the resource. Adobe Pass Authentication handles communicating with the Pay TV provider to obtain authorization. The Programmer needs only to send the request to the Access Enabler and handle the response (success or failure of authorization). If authorization succeeds, an authorization token is stored on the client system, and the callback receives a short-lived media token.

##### Programmer Communication Using the Clientless API {#progr-comm-clientless-api}

Communication between the Programmer's app and Adobe Pass Authentication is via RESTful web services.  There are security protocols in place for all API calls to the Adobe Pass Authentication endpoints.  Security requirements are described in the Clientless API documentation.

##### Sample Workflow With SAML Web Browser SSO-based Authentication {#sample-wf}

1. Viewer Navigates to a site (dummy1.com) and tries to access entitled content.
1. Video page/player loads the Access Enabler from adobe.com and, when prompted by user action, asks for authorization for the requested content.
1. Access Enabler runs and validates the requestor and the request.
1. Access Enabler checks for a valid authorization token in local store. If a valid authorization is found, then the Access Enabler produces a short-lived media token (see step 14).
1. If no valid authorization for the requested resource is found but a valid authentication token exists, then the Access Enabler initiates an authorization request with the Pay TV provider that the user is authenticated against. The Adobe server provisions the authorization request/response exchange with the Pay TV provider.
1. If no valid authentication token is found, the Access Enabler prompts the user for their Pay TV provider. (Selecting a provider that supports the SAML web browser SSO-based authentication triggers a SAML-based authentication workflow. For non-SAML providers, Adobe handles a similar custom workflow.)
1. Access Enabler navigates the browser to Adobe's SAML SP (Service Provider) service, passing it all appropriate parameters.
1. The SAML SP invokes the appropriate SAML IdP (Identity Provider) at the user's Pay TV provider, using the SAML Web browser profile as indicated in the IdP metadata. This effectively navigates the user to the IdP's (Pay TV provider's) site, where the user authenticates.
1. After successful authentication, the user is redirected back to Adobe's SAML SP, passing it an authentication GUID in the SAML response.
1. Adobe's SAML SP creates a session on the server side where the authentication GUID is stored and redirects the user back to the original Programmer page. (The server session is deleted upon Access Enabler retrieval of the authN token.)
1. Access Enabler retrieves the authentication GUID from Adobe's server to include in the token with a device ID maintained by Adobe Pass Authentication. When Flash DRM is on the device, this is done through Flash Access APIs (Flash Player's DRM component) that enable binding of the GUID to the device ID and return an authentication token. Otherwise this is done through JS APIs over HTTPS using HTML5-based storage or via specific native components.
1. The authentication token is used by Access Enabler to make authorization requests to the Pay TV provider. On Flash Access-enabled devices, the requests are always made through Flash Access APIs so that the resulting authorization token is bound to the device. On non-Flash Access devices, HTTPS is used for secure communication from client to server.
1. Upon successful authorization, Adobe Pass Authentication creates a long-lived authorization ("authZ") token and passes it to the Access Enabler, which stores it on the local system.
1. The Access Enabler uses the authZ token to create short-lived media tokens that are used for actual viewing access. For security, these short-lived tokens must be validated by another Adobe Pass Authentication component, the Media Token Verifier.
 
![](../assets/authn-authz-entitlmnt-flow.png)


*Figure 4: Authentication and authorization Access Enabler workflow*  

##### Providing an Entitlement User Interface {#entitlement-ui}

Programmers must create their own UI for the access workflow into their website or app. Some elements, such as the actual login process, are provided by the Pay TV provider, and some elements are optionally available as part of Adobe Pass Authentication. At minimum, the Programmer does the following:

* **Implements a provider selection interface** that allows a new user to identify their Pay TV provider and log in for the first time. For development, the Access Enabler provides a basic user interface that gives the customer a choice of Pay TV providers and initiates the login process. For a production environment, Programmers must implement their own provider selector dialog. Some Pay TV providers redirect to their own site for the login, and some require their login pages to be displayed within an iframe. Programmers must implement the callback that creates this iframe, in case the customer chooses one of those providers.
* **Identifies protected resources.** Protected resources are those that require authorization to access. In offering these resources, the Programmer interface should indicate the need for authorization prior to viewing. With authorization success, the interface should show that the resource is now authorized.
* **Creates and maintains a listing of Pay TV providers** to control user access to only those providers that you specify.
* **Shows that a user is authenticated.** The Programmer should indicate the customer's authentication status as part of whatever means is used to identify protected resources. Programmers can query the Access Enabler to determine whether a customer has already been authenticated.

#### Supporting Single Logout {#single-logout-support}

In most cases, the Programmer is responsible for handling user logouts via a simple API call. The logout() call directs Adobe Pass Authentication to log out the current user by:

* Deleting all AuthN and AuthZ tokens 
* Clearing all authentication and authorization information for that user
* Initiating a Pay TV provider-specific workflow for clearing out the user's authentication session with the provider (for example, if the authentication was done using the SAML Authentication Request protocol, then the logout may be done using the SAML Single Logout protocol.)

If the user leaves their machine idle for enough time that their tokens expire, they can still return to their session and successfully initiate logout. Adobe Pass Authentication ensures that all tokens are deleted and notifies the Pay TV provider to delete their session, as well.
 

When the logout is initiated from a site that isn't integrated with Adobe Pass Authentication, the Pay TV provider can invoke the Adobe Pass Authentication Single Logout service through a browser redirect.

## Beyond the Basic Entitlement Flows - Additional Features {#beyond-basics}

The basic entitlement flows are Start-up, Authentication, Authorization, and Logout.  As Adobe Pass Authentication matures and develops, a number of additional features have been and are being added to the basic flows.  These include:

* **User Metadata** - Depending upon agreements between MVPDs and Programmers, MVPDs can securely exchange metadata such as Zipcode, maximum rating, channel ID, and more. Metadata enables various use cases, including parental controls, regional freeze periods for sports events, etc.
* **Temporary Free Access** - Lets Programmers offer temporary free access to their protected content (for example, short samples of daily programming, or free presentation of a large event).
* **Proxy MVPD** - An MVPD can manage its own integration with Adobe Pass Authentication, and also manage the entitlement process on behalf of a group of associated "ProxiedMVPDs".

## Security {#security}

This section highlights the security and integrity of the Adobe Pass Authentication infrastructure.

### Token Security {#token-security}

One of the primary goals of Adobe Pass Authentication is ensuring that the system can withstand attacks on the content entitlement data by a rogue user or content aggregator. Therefore, data access is secured at different levels in the workflow, with protecting the generation and usage of the authorization token data having the highest importance. The Adobe Pass Authentication architecture is designed to ensure token contents are securely maintained and that the token remains on the device to which it was issued.

* **Long-lived AuthN and AuthZ token security** - All long-lived tokens are digitally signed by the Adobe Pass Authentication server. The digital signature, however, differs from platform to platform, in that it uses a device ID that differs in how it is generated, protected, and validated. In all cases, a client-side validation ensures that the digital signature is intact, and that the integrity of the token is preserved. The Access Enabler securely stores the validated tokens in locations specific to the environment in which it is running. If device ID validation fails, the authentication session is invalidated, tokens are reset, and the user is prompted to log in again.
* **Short-lived Media token security** - Short-lived media tokens, which are produced in the final step prior to content access, are signed by Adobe and encrypted to avoid tampering during exchange. Short-lived Media tokens also require an extra validation step by an additional Adobe Pass Authentication component, the Media Token Verifier. The TTL of the short-lived token is set to a default of 5 minutes and can be made shorter, if desired. The short-lived Media token is never cached; a new token is retrieved from the server every time an authorization API is called. 

### Platform-specific Device Security {#platform-sp-security}

The security measures used by Adobe Pass Authentication vary by platform, but all are robust and state-of-the-art.

* **Flash-enabled devices** - When Flash Player 10.1+ or AIR 2.5+ is on the device, Adobe Pass Authentication uses the Flash Player DRM functionality for protection, also known as Flash Access. Flash provides an extra level of protection; the strong assurance of device binding for Flash-based tokens means that in most cases, the time-to-live can be longer, the user does not have to log in as often, and the user experience is generally smoother.
* **In-browser experiences on HTML5-capable devices**- On non-Flash devices that include HTML5 browser capability, Adobe Pass Authentication has an alternative means of limited protection for browser-based integrations. However, because the device binding for HTML5 is not as strong, the time-to-live (TTL) for tokens on HTML5 platforms is typically shorter.
* **Native app support for  in- and out-of-home devices** - Adobe offers native SDKs per OS (iOS, Android, Windows 8, etc.) that provide enhanced security over the HTML5 solution. These SDKs use native APIs to retrieve a Device ID and pass it securely to the Adobe Pass Authentication server.
* **Clientless** - Adobe Pass Authentication uses the HTTPS protocol for secure communication. In addition, all calls from a smart device must be digitally signed.

## FAQ {#faqs}

**What is TV Everywhere?**
The industry movement known as TV Everywhere enables pay TV customers to access the premium content they already subscribe to on a variety of Internet-connected devices, including personal computers, tablets, smartphones, game consoles, set-top boxes, and "Smart" TVs. The challenge of this initiative is to make the authentication process is as simple and painless as possible, allowing customers to smoothly access their subscription content without prohibitive barriers and multiple logins.
 

**What is Adobe Pass Authentication, and how does it relate to TV Everywhere?**
Adobe Pass Authentication takes TV Everywhere from concept to reality by smoothly verifying a user's entitlement to content in a manner that is both simple and secure. Adobe Pass Authentication is a hosted service that allows rapid back-end integration based on the business rules required by both Programmers and Pay TV providers. This means a quick time to market for all parties, a more secure environment to prevent fraud, and a superior customer experience, with more TV content available to more people across more platforms.
 

**How is Adobe Pass Authentication offered/delivered?**
Adobe Pass Authentication is offered via the Software as a Service (SaaS) model. This enables more secure communication to take place between end users, Programmers, and Pay TV providers in order to validate entitlement to content. The core components of the service include the client-side Access Enabler (or the Clientless API for some devices) and the hosted Adobe Pass Authentication Server. The Access Enabler is a small file that is loaded into a Programmer's web page or player application. It communicates with the Adobe Pass Authentication Servers, which in turn have connections built into the authentication systems of various Pay TV providers. Adobe Pass Authentication also offers a Clientless API approach to integration for some "smart devices" that aren't web-capable (Smart TVs, Set-top Boxes, Game Consoles, etc.). The Clientless approach provides RESTful web services with which developers can implement the Adobe Pass Authentication entitlement flows on these devices.
 

**How is Adobe Pass Authentication different from other TV Everywhere solutions?**
Adobe Pass Authentication has distinct benefits over alternative TV Everywhere solutions. Direct integrations with individual providers do not provide the flexibility of a single, persistent login (SSO) as users travel from site to site across the Internet. Adobe Pass Authentication also has remarkable market penetration; once a Programmer integrates with Adobe Pass Authentication, they are immediately connected with Pay TV operators serving over 90% of the households in the United States. Additionally, Adobe Pass Authentication leverages unique security features built into the Flash runtime (where available) to help mitigate fraud, while also providing SDKs so that Programmers can have the same TV Everywhere functionality built into native apps for mobile or in-home devices where Flash is not available. Finally, while Adobe Pass Authentication is available as a standalone service, we also offer the option to have tight integration with other Adobe products and services (including Adobe Pass and Adobe Analytics) related to the delivery, protection, and monetization of TV Everywhere content.
 
**How secure is Adobe Pass Authentication?**
The number one priority of the Adobe Pass Authentication architecture is to ensure that only authorized viewers are authenticated and granted access to premium content. Adobe Pass Authentication tightly binds access to viewing device and can help to limit streams, sessions, and/or devices for a given household.
 

**Is Flash Player required?**
Adobe Flash Player 11.x or later is required for the strictest device binding security. However, Adobe Pass Authentication for TV Everywhere is player and platform agnostic, integrating with any playback application, including Silverlight and HTML5. Additionally, Adobe Pass Authentication provides native support for devices such as iOS, Android, and Xbox where Flash Player is not available.  Finally, Adobe Pass Authentication provides a Clieintless approach for devices that are not capable of rendering web page (game consoles, Smart TVs, Set-top boxes).
 

**Which devices does Adobe Pass Authentication support?**
Adobe Pass Authentication is supported by virtually any device with the HTML5 web kit for in-browser viewing experiences. Additionally, Adobe Pass Authentication is continuing to roll out native software development kits (SDKs) for various device-specific platforms, including iOS, Android&trade;, and Windows 8. Adobe Pass Authentication partially supports some non-web-capable devices (Smart TVs, Set-top boxes, game consoles, etc.) through its RESTful web services APIs. 

**Does Adobe Pass Authentication support the emerging standards for TV Everywhere?**
Adobe Pass Authentication is compliant with the **CableLabs OLCA (Online Content Access)** [specification](https://www.cablelabs.com/specifications), which provides technical requirements and architecture for the delivery of video to a Pay TV customer from online sources. Adobe participated in the joint CableLabs interopt testing project in June 2011 and passed the testing process for a Service Provider implementation. Adobe Pass Authentication is verified (complete and tested) against the OLCA specifications for authentication. The authorization component is completed, but testing verification awaits the release of the CableLabs testing environment (ETA Nov 2011). 

Adobe is also an active member of the **OATC (Open Authentication Technical Consortium)** and participates in several of the subcommittees' specification-drafting projects as part of that body. 

**How does Adobe Pass Authentication handle federated identity management/single sign-on (SSO)?**
Adobe Pass Authentication allows you to provide customers with single sign-on (SSO) authentication and authorization, using back-channel (server-to-server) communication between Adobe Pass Authentication and participating Pay TV operators. So, with Adobe Pass Authentication, there's no need for subscribers to log in again after their first authentication, for as long as that authentication is allowed by the Pay TV operator to persist. Typically this limit is set at 30 days. To accomplish this, Adobe Pass Authentication provides a common domain for authentication tokens for our customers. This authentication state information is available to all participating sites that are integrated with a given Pay TV operator. 

Currently, most Adobe Pass Authentication integrations with Pay TV operators use the SAML protocol, one of the primary authentication standards. Adobe Pass Authentication acts as a proxy Service Provider in the SAML architecture and persists the SAML authentication response as a secure token in the Adobe common domain. Adobe Pass Authentication is SAML 2.0 compliant. 

While Adobe Pass Authentication is typically used with SAML SSO solutions at this point, the Adobe Pass Authentication architecture abstracts any protocol specifics from the Programmer integration. Therefore, support for new protocols-such as one based on OAuth 2.0 or custom protocols-can be added over time. 

**How much does Adobe Pass Authentication for TV Everywhere cost for end users?**
There is no additional cost to end users for use of Adobe Pass Authentication.

>[!NOTE]
>
>**Next steps:** For more information, contact your Adobe representative or fill out the Request for Information form [here](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi).
>
