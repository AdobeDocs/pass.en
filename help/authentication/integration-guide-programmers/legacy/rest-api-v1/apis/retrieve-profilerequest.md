---
title: Retrieve Platform SSO profile-request
description: Retrieve Platform SSO profile-request
exl-id: 44fd4e26-4d9a-4607-ac2c-b85d848f5fc6
---
# (Legacy) Retrieve Platform SSO profile-request {#retrieve-platform-sso-profile-request}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md)

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

This resource produces profile requests for a requestor ID and MVPD tuple.

  
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/{requestor}/profile-requests/{mvpd} | Streaming App</br></br>or</br></br>Programmer Service | 1. requestor (path param)</br>2. mvpd (path param)</br>3. deviceType (Mandatory) | GET | The response Content-Type will be application/octet-stream, as the actual payload is opaque for the client application.</br></br>The response should be forwarded by the application to the Platform</br></br>SSO engine for obtaining a Profile SSO. | 200 - Success   </br>400 - Bad request |


| Input Parameter | Description                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| requestor       | The Programmer requestorId for which this operation is valid.                                            |
| mvpd            | The MVPD Id for which this operation is valid.                                                           |
| deviceType      | The Apple platform for which we are attempting to obtain a profile-request.  Either **iOS** or **tvOS**. |
