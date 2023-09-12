---
title: Initiate Authorization
description: Initiate Authorization
exl-id: 2f8a5499-e94f-40dd-9fb0-aac8e080de66
---
# Initiate Authorization {#initiate-authorization}

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

Obtains authorization response. 

| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/authorize | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>2.  deviceId (Mandatory)</br>3.  resource (Mandatory)</br>4.  device_info/X-Device-Info (Mandatory)</br>5.  _deviceType_</br>6.  _deviceUser_ (Deprecated)</br>7.  _appId_ (Deprecated)</br>8.  extra parameters (Optional) | GET | XML or JSON containing authorization details or error details if unsuccessful. See samples below. | 200 - Success  </br>403 - No Success |

{style="table-layout:auto"}

</br>


| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| resource | A string that contains a resourceId (or MRSS fragment), identifies the content requested by a user and is recognized by MVPD authorization endpoints. |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | The device type (e.g. Roku, PC).</br></br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.</br></br>See [Benefits of clientless device type parameter in pass metrics](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Note**: the device_info will replace this parameter. |
| _deviceUser_ | The device user identifier. |
| _appId_ | The application id/name. </br></br>**Note**: the device_info replaces this parameter. |
| extra parameters | The call may also contain optional parameters that enable other functionalities like:</br></br>* generic_data - enables the use of [Promotional TempPass](/help/authentication/promotional-temp-pass.md)</br></br>Example: `generic_data=("email":"email@domain.com")` |

{style="table-layout:auto"}

>[!CAUTION]
>
>**Streaming Device IP Address**</br>
>For Client-to-Server implementations, the Streaming Device IP Address is implicitly sent with this call.  For Server-to-Server implementations, where the **regcode** call is made by the Programmer Service and not the Streaming Device, the following header is required to pass the Streaming Device IP Address:</br></br>
>
>```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>where `<streaming\_device\_ip>` is the Streaming Device public IP address.</br></br>
>Example :</br>
>
>```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```
>


### Sample Response {#sample-response}

* **Case 1: Success**
</br>
  * **XML:**
  </br>
  
    ```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
    <expires>1348148289000</expires>
    <mvpd>sampleMvpdId</mvpd>
    <requestor>sampleRequestorId</requestor>
    <resource>sampleResourceId</resource>
    </authorization>
    ```



  * **JSON:**

    ```JSON
    {
      "mvpd": "sampleMvpdId",
      "resource": "sampleResourceId",
      "requestor": "sampleRequestorId",
      "expires": "1348148289000"
    }
    ```

  >[!IMPORTANT]
  >
  >When the response comes from a Proxy MVPD, it may include an additional element named `proxyMvpd`. 

 

* **Case 2: Authorization denied**


  ```JSON 
  <error>
    <status>403</status>
    <message>User not authorized</message>
    <details>Your subscription package does not include the "ASFAFD" channel.
    Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
  </error>
  ```
