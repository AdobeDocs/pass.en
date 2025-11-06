---
title: Free Preview for Temp Pass and Promotional Temp Pass
description: Free Preview for Temp Pass and Promotional Temp Pass
exl-id: c584bf0c-15c4-4a4d-b6a2-8d15ee786fe3
---
# (Legacy) Free Preview for Temp Pass and Promotional Temp Pass {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

Allows the creation of an authentication token for Temp Pass and Promotional Temp Pass without the need for a second screen.

  
| Endpoint                                  | Called  </br>By                                       | Input   </br>Params                                                                                                                                                                                                                                                                                                                             | HTTP  </br>Method | Response                                                                                                                                      | HTTP  </br>Response                       |
|-------------------------------------------|-------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| <SP_FQDN>/api/v1/authenticate/freepreview | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor_id (Mandatory)</br>    </br>2.  deviceId (Mandatory)</br>    </br>3.  mso_id (Mandatory)</br>    </br>4.  domain_name (Mandatory)</br>    </br>5.  device_info/X-Device-Info (Mandatory)</br>6.  deviceType</br>    </br>7.  deviceUser (Deprecated)</br>    </br>8.  appId (Deprecated)</br>    </br>9.  generic_data (Optional) | POST              | The successful response will be a 204 No Content, indicating that the token was successfully created and is ready to use for the authz flows. | 204 - No Content   </br>400 - Bad request |

<div>

  
| Input Parameter                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| requestor_id                        | The Programmer requestorId for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| deviceId                            | The device id bytes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| mso_id                              | The MVPD Id for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| domain_name                         | The domain name for which a token will be granted. This is being compared with the domains of the service provider when an authorization token is being granted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br>See the full details in [Passing Device and Connection Information](/help/authentication/integration-guide-programmers/legacy/client-information/passing-client-information-device-connection-and-application.md).                                                                                                                                                                                                            |
| _deviceType_                        | The device type (e.g. Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.</br></br>See [Benefits of using clientless device type parameters](/help/authentication/integration-guide-programmers/legacy/notes-technical/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Note**: the device_info will replace this parameter. |
| _deviceUser_                        | The device user identifier.</br></br>**Note**: If used, deviceUser should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                                                                                                              |
| _appId_                             | The application id/name. </br></br>**Note**: the device_info replaces this parameter. If used, `appId` should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                                                                          |
| generic_data                        | Used to limit the scope of the token for Promotional Temp Pass.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |


### [Back to REST API Reference](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/rest-api-reference.md)
