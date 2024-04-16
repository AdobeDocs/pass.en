---
title: REST API Cookbook (Server-to-Server)
description: Rest API cookbook server to server.
exl-id: 36ad4a64-dde8-4a5f-b0fe-64b6c0ddcbee
---
# REST API Cookbook (Server-to-Server) {#rest-api-cookbook-server-to-server}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Overview {#overview}

The purpose of this cookbook document is to detail best practices for implementing Adobe Pass Authentication using the Server-to-Server architectures.  It provides basic requirements, step-by-step flow implementation and general considerations for production environments and operation.

### Throttling mechanism

The Adobe Pass Authentication REST API is governed by a [Throttling mechanism](/help/authentication/throttling-mechanism.md).
 

## Components {#components}

In a working Server-to-Server solution the following components are involved:

 
| Type | Component | Description |
| --- | --- | --- |
| Streaming Device | Streaming App | The Programmer application that resides on the user's streaming device and plays authenticated video. |
| | \[Optional\] AuthN Module | if Streaming Device has a User Agent (i.e. Web Browser), the AuthN Module is resposnible for authenticating the user on the MVPD IdP. |
| \[Optional\] AuthN Device | AuthN App | if the Streaming Device does not have a User Agent (i.e. Web Browser), the AuthN Application is a Programmer web application that is accessed from a separte user's device using a web browser. |
| Programmer Infrastructure | Programmer Service | A service that links the Streaming Device with the  Adobe Pass Service to obtain authentication and authorization decisions. |
| Adobe Infrastructure | Adobe Pass Service | A service that integrates with the MVPD IdP and AuthZ Service and provides authentication and authorization decisions. |
| MVPD Infrastructure | MVPD IdP | An MVPD endpoint that provides credential-based authentication service to validate their user's identity. |
| | MVPD AuthZ Service | An MVPD endpoint that provides authorization decisions based on user's subscriptions, parental controls, etc. |


Additional terms used in the flow are defined in the
[Glossary](/help/authentication/glossary.md).

## Flows {#flows}

### Dynamic Client Registration (DCR)


Adobe Pass uses DCR to secure client communications between a programmer application or server and the Adobe Pass services. The DCR flow is separate, dependent and prerequisite flow and can be found in [Dynamic Client Registration](/help/authentication/dynamic-client-registration.md).


### Authentication (authN)

The authentication flow is used to allow a user to identify themselves
to their MVPD to determine whether the user has a valid account. 

1.  The user starts the Streaming Device app and attempts to login or view protected content.
2.  The Streaming Device app makes request to the Programmer Service to determine whether the device is already authenticated.
3.  The Programmer Service registers the app using DCR.
4.  The Programmer Service checks the Streaming Device authN status by calling the Adobe Pass Service **checkauthn** API.
5.  For the case where the **checkauthn** call returns the status that the User Device is authenticated, then the app can proceed to the Authorization flow.
6.  For the case where the **checkauthn** call returns the status that the User Device is NOT authenticated, then the app should wait for a user request to login.
7.  When the user requests to directly login (e.g. selects login button) or indirectly login (e.g. selects protected content when not already authenticated), the Streaming Device app makes a request to the Programmer Service to initiate user authentication. The Programmer Service requests and receives a unique registration code (regcode) by calling the Adobe Pass Service **regcode** API.
8.  The Programmer Service also retrieves the list of current MVPDs and attributes by calling the Adobe Pass Service **config** API. Note: this API can also be called earlier in the flow and cached.
9.  The Programmer Service returns the regcode to the Streaming Device app and the processed MVPD list requested in step \#7. Note: The processed MVPD list format is specified by the Programmer and can be filtered to explicitly allow or block specific MVPDs (i.e. allow- or block-lists).
10. If the is different from the AuthN Device (i.e. "second screen"), either by choice or necessity (i.e. the Streaming Device does not support a User Agent), then the Streaming Device should display the regcode and a URI for the user to accesss the AuthN Application. The user types the URI into the User Agent on the AuthN Device to launch the AuthN Application, and then types the regcode into that application. If the Streaming Device is the same as the AuthN Device, then the regcode can be programmatically passed to the AuthN Module.
11. The AuthN Module initiates the user authentication with the MVPD by displaying an MVPD Picker. After the user selects the MVPD, the AuthN Module calls **authenticate** with the regcode, which redirects the User Agent to the MVPD IdP. When the user successfully authenticates with the MVPD, the User Agent is redirected back through the Adobe Pass Service, where the successful authentication is recorded with the regcode, and is then redirected back to the AuthN Module.
12. If the Streaming Device is different from the AuthN Device, then the AuthN Device should display a successful authentication message to the user and steps to continue (e.g. "Success\! You can now return to your game console to continue \[...\]"). If the Streaming Device is the same as the AuthN Device, then the Streaming Device may programmatically detect the authentication completion.

 

The following diagram illustrates the authentication flow:

![](assets/authn-flow.png)

### Authorization (authZ)

The authorization flow is used to determine whether a user is entitled to access requested content.

1. Every time the user attempts to view protected content on the Streaming Device app, the Streaming Device app calls the Programmer Service identifying the content and requesting permission and information needed to start the stream.
1. The Programmer Service calls the Adobe Pass **authorize** API passing the Resource ID along with other required parameters. The Adobe Service calls the MVPD AuthZ Service with the Resource ID and receives and authorization decision that is then passed back to the Programmer Service. This authorization decision will be cached by the Adobe Pass Service for a configurable period. On subsequent **authorize** calls from the Programmer Service to the Adobe Pass Service, the cached value will be returned as long as it is valid.
1. If the authorization is granted, the Programmer Service should call the Adobe Pass **/tokens/media** API, which will return a signed media token. The Programmer Service should validate the media token using the Media Token Verifier library (JAR). If valid, the Programmer Service should return permission and the needed to start the stream (e.g. stream URL) requested in step \#1.
1. If the authorization is denied, the **authorize** call will return an error code and description to the Programmer Service. The Programmer Service should return the error code and description (or a Programmer modified message) to the request in step \#1.

The following diagram illustrates the authorization flow:

![](assets/authz-flow.png)

### Logout

The logout flow allows a user to remove the identity currently
associated with the application.

1. When the user requests to logout (i.e. remove from the device the current MVPD account associated with the application), the Streaming Device app calls the Programmer Service telling it to logout the device.
1. The Programmer Service should call the Adobe Pass **logout** API.

The following diagram illustrates the logout flow:

![](assets/logout-flow.png)

### \[Optional\] Preauthorization (a.k.a. Pre-flight)

Preauthorization can be used to quickly determine from a set of resources the ones a user might have access.  The result of this call is typically used to customize the UI for an individual user.

1.  Once the user is authenticated, the Steaming Device may call the Programmer Service to request the content to which the user is entitled to stream.

1.  The Programmer Service should call the Adobe Pass **preauthorize** API with a list of Resource IDs, which are a simple string that typically represent a channel a user might be entitled to stream. *Note: Currently, the* ***preauthorize*** *call is configured to limit the list to five (5) Resource IDs. When more than five resources are needed, multiple* ***preauthorize*** *calls can be made, or the call can be configured to accept more than five resources with an agreement from the MVPDs. Implementors should keep in mind the cost of a* ***preauthorize*** *call both to MVPD resources as well as the response time to the Programmer and structure their use of the call judiciously.*

1.  The **preauthorize** call will respond to the Programmer Service with a JSON object containing a TRUE or FALSE value for each Resource ID in the request that indicates whether the user is entitled to the associated channel or not. *Note: If an MVPD does not provide an answer for a given Resource ID (e.g. because of network errors or time outs), the value will default to FALSE.*

1.  The Programmer Service should use the **preauthorize** call response to create a Programmer-defined custom response to the Streaming Device, typically to personalize the presentation to the user based on their entitlements.

The following diagram illustrates the preauthorization flow:

![](assets/preauthz-flow.png)


### \[Optional\] Metadata

Metadata can be used to retrieve user information shared by the MVPD.
 Examples of this might include user ID, zip code, etc.

1.  Once the user is authenticated, Programmer Service may call the Adobe Pass **usermetadata** API to request information about the authenticated user.

1.  The response will include all metadata available for the given user. The specific fields are configured separately for each Programmer/MVPD integration.

The following diagram illustrates the preauthorization flow:

 

![](assets/user-metadata-api-preauthz.png)

 

## Environments and Functional Requirements{#environments}

 

A Programmer should create at least two environments: one for production, and one or more for staging.


### Production

The production environment should be highly available and scaled appropriately for large or unexpected spikes (e.g. live sports, breaking
news).

 

The Adobe Pass service runs on multiple data centers geographically dispersed throughout the US.  To achieve the best response time (i.e. lowest latency) from the Adobe Pass service, the Programmer should also create a similar geographically dispersed service
infrastructure. 

  
The Programmer service should limit the DNS cache to a maximum of 30s in case Adobe needs to reroute traffic. This may occur if a data center becomes unavailble.  
 

The Programmer should provide the public IP range of the production environment. These will be entered into an allowed-list of IPs in Adobe Pass infrastructure for access and managed by Adobe's Fair API usage policies.

### Staging

The staging environment can be minimal, but should include all system components and business logic. It should function similarly to production and allow for testing releases outside of production. Ideally, the staging environment can be connected to the Adobe Pass testing environments for use by the Programmer, and by Adobe when needed so we can assist in testing and troubleshooting.

### Functional Requirements

The Programmer service must pass along accurate device identification information for the device for which they are executing the flows. Additionally, the Programmer service must pass the IP of the device for which they are executing the flows (in an x-forwarded-for header) along with the connection source port (in the device info field):

    **X-Forwarded-For : \<client\_ip\>** 

    where \<client\_ip\> is the client public IP address

     

    The header needs to be added on **regcode** and **authorize** calls

    Examples :

    POST /reggie/v1/{req\_id}/regcode HTTP/1.1

    X-Forwarded-For:203.45.101.20

     

    GET /api/v1/authorize HTTP/1.1

    X-Forwarded-For:203.45.101.20

 

The Programmer service should send data and formating required by individual MVPDs or integrated apps (e.g. device IP, source port, device information, MRSS, optional data such as ECID). <!--Please see the documentation for [Passing Device and Connection Information Cookbook](http://tve.helpdocsonline.com/passing-device-information-cookbook)-->.


The Programmer service must respect authN and authZ TTLs when caching and invalidate the authN or authZ sessions when notified.

The Programmer must maintain certificates shared with Adobe.

<!--
## Related Information {#related}

* [REST API Reference](/help/authentication/rest-api-reference.md)
* [Glossary of Terms](/help/authentication/adobe-pass-glossary.md)
-->
