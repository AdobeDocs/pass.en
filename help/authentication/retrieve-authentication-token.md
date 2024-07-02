---
title: Retrieve Authentication Token
description: Retrieve Authentication Token
exl-id: 7fb03854-edad-41e7-b218-1858fc071876
---
# Retrieve Authentication Token {#retrieve-authentication-token}

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

Retrieves authentication (AuthN) Token.  
 
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/tokens/authn</br></br>For example:</br></br><SP_FQDN>/api/v1/tokens/authn | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>2.  deviceId (Mandatory)</br>3.  device_info/X-Device-Info (Mandatory)</br>4.  _deviceType_ (Deprected)</br>5.  _deviceUser_ (Deprecated)</br>6.  _appId_ (Deprecated) | GET | XML or JSON containing authentication information or error details if unsuccessful. | 200 - Success.  </br>404 - Token Not Found  </br>410 - Token expired |

{style="table-layout:auto"}


| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| device_info/</br></br>X-Device-Info | Streaming Device information.</br></br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br>See the full details in [Passing Device and Connection Information](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | The device type (for example, Roku, PC).</br></br>**Note**: the device_info replaces this parameter. |
| _deviceUser_ | The device user identifier.</br></br>**Note**: If used, deviceUser should have the same values as in the [Create Registration Code](/help/authentication/registration-code-request.md) request. |
| _appId_ | The application id/name. </br></br>**Note**: the device_info replaces this parameter. If used, `appId` should have the same values as in the [Create Registration Code](/help/authentication/registration-code-request.md) request. |

{style="table-layout:auto"}

</br>

### Sample Response {#response}

 

#### Success

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authentication>
         <expires>1601114932000</expires>
         <userId>sampleUserId</userId>
         <mvpd>sampleMvpdId</mvpd>
         <requestor>sampleRequestor</requestor>
    </authentication>
```


**JSON:**

```JSON
    {
         "requestor": "sampleRequestor",
         "mvpd": "sampleMvpdId",
         "userId": "sampleUserId",
         "expires": "1601114932000"
    }
```

 

 

#### Authentication Token not found:

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 
**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found"
    }
```
