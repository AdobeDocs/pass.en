---
title: Initiate Logout
description: Initiate logout
exl-id: 9625b5a2-31d9-4e20-8703-4a9e4eeb1618
---
# (Legacy) Initiate Logout {#initiate-logout}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

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

Remove AuthN and AuthZ tokens from storage.

 
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/logout | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor</br>2.  deviceId (Mandatory)</br>3.  device_info/X-Device-Info (Mandatory)</br>4.  _deviceType_</br>5.  _deviceUser_ (Deprecated)</br>6.  _appId_ (Deprecated) | DELETE | None | 204 |

  
| Input Parameter                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| requestor                           | The Programmer requestorId for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| deviceId                            | The device id bytes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br>See the full details in [Passing Device and Connection Information](/help/authentication/integration-guide-programmers/legacy/client-information/passing-client-information-device-connection-and-application.md).                                                                                                                                                                                                          |
| _deviceType_                        | The device type (e.g. Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.</br></br>See [Benefits of using the clientless device type parameter in pass metrics](/help/authentication/integration-guide-programmers/legacy/notes-technical/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Note**: the device_info will replace this parameter. |
| _deviceUser_                        | The device user identifier.</br></br>**Note**: If used, deviceUser should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                                                                                                               |
| _appId_                             | The application id/name. </br></br>**Note**: the device_info replaces this parameter. If used, `appId` should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                                                                           |

>[!IMPORTANT] 
> 
>The logout call currently has the following limitation: it clears the AuthN and AuthZ tokens from storage (i.e., on the Programmer / Adobe Pass Authentication side), but **does not** call the MVPD logout endpoint.
