---
title: Check Authentication Token
description: Check Authentication Token
exl-id: 9020f261-44d8-4bd5-b85b-a8667679f563
---
# Check Authentication Token {#check-authentication-token}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

Indicates whether the device has an unexpired authentication token.

| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/checkauthn | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>2.  deviceId (Mandatory)</br>3.  device_info/X-Device-Info (Mandatory)</br>4.  _deviceType_ </br>5.  _deviceUser_ (Deprecated)</br>6.  _appId_ (Deprecated) | GET | XML or JSON containing error details if unsuccessful. | 200 - Success   </br>403 - No Success |

{style="table-layout:auto"}


| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL parameter, but due to the potential size of this parameter and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)(/help/authentication/passing-client-information-device-connection-and-application.md)-->. |
| _deviceType_ | The device type (e.g. Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.</br></br>For details, see [Benefits of using the Clientless deviceType parameter in Primetime authentication metrics](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br>**Note**: the device_info will replace this parameter. |
| _deviceUser_ | The device user identifier. |
| _appId_ | The application id/name.</br>**Note**: the device_info replaces this parameter. |

{style="table-layout:auto"}


## Response (if unsuccessful) {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [Back to REST API Reference](/help/authentication/rest-api-reference.md)
