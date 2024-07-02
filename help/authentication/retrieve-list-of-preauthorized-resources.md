---
title: Retrieve List of Preauthorized Resources
description: Retrieve List of Preauthorized Resources
exl-id: 3821378c-bab5-4dc9-abd7-328df4b60cc3
---
# Retrieve List of Preauthorized Resources {#retrieve-list-of-preauthorized-resources}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/throttling-mechanism.md)

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

A request to Adobe Pass Authentication to obtain the list of preauthorized resources.

There are two sets of APIs: one set for the Streaming App or Programmer Service and one set for the Second Screen Web App. This page describes the API for the Streaming App or Programmer Service.

  
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/preauthorize | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>2.  deviceId (Mandatory)</br>3.  resource list (Mandatory)</br>4.  device_info/X-Device-Info (Mandatory)</br>5.  _deviceType_</br>6.  _deviceUser_ (Deprecated)</br>7.  _appId_ (Deprecated) | GET | XML or JSON containing individual pre-authorization decisions or error details. See samples below. | 200 - Success</br></br>400 - Bad request</br></br>401 - Unauthorized</br></br>405 - Method not allowed  </br></br>412 - Precondition failed</br></br>500 - Internal Server Error |

  
| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| resource list | A string that contains a comma delimited list of resourceIds that identifies the content that might be accessible to a user and is recognized by MVPD authorization endpoints. |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br>See the full details in [Passing Device and Connection Information](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | The device type (for example, Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for example, Roku, AppleTV, and Xbox.</br></br>See, [benefits of using clientless device type parameter in pass metrics](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Note**: the `device_info` will replace this parameter. |
| _deviceUser_ | The device user identifier. |
| _appId_ | The application id/name. </br></br>**Note**: the device_info replaces this parameter. |



### Sample Response {#sample-response}

 

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
  <resource>
    <id>TestStream1</id>
    <authorized>true</authorized>
  </resource>
  <resource>
    <id>TestStream2</id>
    <authorized>false</authorized>
    <error>
      <status>403</status>
      <code>authorization_denied_by_mvpd</code>
      <message>User not authorized</message>
      <details>Your subscription package does not include the "TestStream3" channel.</details>
      <helpUrl>https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes</helpUrl>
      <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
      <action>none</action>
    </error>
  </resource>
</resources>
```
 
</br>

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
