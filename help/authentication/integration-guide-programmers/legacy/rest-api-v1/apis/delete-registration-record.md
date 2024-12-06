---
title: Delete Registration Record
description: Delete registration resord
exl-id: 42707070-2e1f-4847-93fd-30025aef56c1
---
# Delete Registration Record {#delete-registration-record}

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


## Description {#delete-record}

Deletes the reg code record and releases the reg code for reuse. 

| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <REGGIE_FQDN>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>For example:</br></br><REGGIE_FQDN>/reggie/v1/regcode/ER45RTY | Streaming App</br></br>or</br></br>Programmer Service | 1.  Requestor ID  </br>    (Path component)</br>2.  Registration code  </br>    (Path component) | DELETE | None | 204 |

{style="table-layout:auto"}

</br>

| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| registration code | The registration code value that would be displayed on the Streaming Device (to be entered into the authentication flow). |

{style="table-layout:auto"}

</br>

### [Back to REST API Reference](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/rest-api-reference.md)
