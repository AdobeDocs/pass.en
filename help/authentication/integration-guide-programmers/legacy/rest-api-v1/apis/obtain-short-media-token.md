---
title: Obtain Short Media Token
description: obtain short media token
exl-id: 667eaaba-423e-4d54-9dbe-084b3c049e1f
---
# Obtain Short Media Token {#obtain-short-media-token}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md)

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* Staging - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* Staging - [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

Obtains Short Media Token.  

| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/mediatoken</br></br>  or</br></br><SP_FQDN>/api/v1/tokens/media</br></br>For example:</br></br><SP_FQDN>/api/v1/tokens/media | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>2.  deviceId (Mandatory)</br>3.  resource (Mandatory)</br>4.  device_info/X-Device-Info (Mandatory)</br>5.  _deviceType_</br>6.  _deviceUser_ (Deprecated)</br>7.  _appId_ (Deprecated) | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>
  
| Input Parameter                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| requestor                           | The Programmer requestorId for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| deviceId                            | The device id bytes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| resource                            | A string that contains a resourceId (or MRSS fragment), identifies the content requested by a user and is recognized by MVPD authorization endpoints.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br>See the full details in [Passing Device and Connection Information](/help/authentication/integration-guide-programmers/passing-client-information-device-connection-and-application.md).                                                                                                                                                     |
| _deviceType_                        | The device type (for example, Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for. For example, Roku, AppleTV, and Xbox.</br></br>See [Benefits of using clientless devicetype parameter](/help/authentication/notes-technical/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Note**: the device_info will replace this parameter. |
| _deviceUser_                        | The device user identifier.</br></br>**Note**: If used, deviceUser should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                                                          |
| _appId_                             | The application id/name. </br></br>**Note**: the device_info replaces this parameter. If used, `appId` should have the same values as in the [Create Registration Code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) request.                                                                                                                                                                                                                                                                                                                      |

{style="table-layout:auto"}

### Sample Response {#response}

**XML:**

```XML 
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <play>
        <expires>1348649569000</expires>
        <mvpdId>sampleMvpdId</mvpdId>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <serializedToken>PHNpZ25hdH[...]</serializedToken>
        <userId>sampleScrambledUserId</userId>
    </play>
```



**JSON:**

```JSON 
    {
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348649614000",
        "serializedToken": "PHNpZ25hdH[...]",
        "userId": "sampleScrambledUserId",
        "mvpdId": "sampleMvpdId"
    }
```

 

### Media Verification Library compatibility

The field `serializedToken` from the "Obtain Short Media Token" call is a Base64 encoded token that can be verified against the Adobe Media Verification Library.
