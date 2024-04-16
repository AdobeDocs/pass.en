---
title: Registration Page
description: Registration Page
exl-id: 581b8e2e-7420-4511-88b9-f2cd43a41e10
---
# Registration Page {#registration-page}

## REST API Endpoints {#clientless-endpoints}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/throttling-mechanism.md)

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Description {#create-reg-code-svc}

Returns randomly generated registration Code and Login Page URI.

| Endpoint | Called  </br>By | Input   </br>Parameter | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <REGGIE_FQDN>/reggie/v1/{requestor}/regcode</br>For example:</br>REGGIE_FQDN/reggie/v1/sampleRequestorId/regcode | Streaming App</br>or</br>Programmer Service | 1.  requestor  </br>    (Path component)</br>2.  deviceId (Hashed)   </br>    (Mandatory)</br>3.  device_info/X-Device-Info (Mandatory)</br>4.  mvpd (Optional)</br>5.  ttl (Optional)</br>6.  _deviceType_</br>7.  _deviceUser_ (Deprecated)</br>8.  _appId_ (Deprecated) | POST | XML or JSON containing a registration code and information or error details if unsuccessful. See schemas and samples below. | 201 |

{style="table-layout:auto"}

| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| device_info/</br>X-Device-Info | Streaming Device information.</br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br>See the full details in [Passing Device and Connection Information](/help/authentication/passing-client-information-device-connection-and-application.md). |
| mvpd | The MVPD ID for which this operation is valid. |
| ttl | How long this regcode should live in seconds.</br>**Note**: The maximum value allowed for ttl is 36000 seconds (10 hours). Higher values result in a 400 HTTP response (bad request). If `ttl` is left empty, Adobe Pass Authentication sets a default value of 30 minutes. |
| _deviceType_ | The device type (e.g. Roku, PC).</br>If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for example, Roku, AppleTV, and Xbox.</br>See, [Benefits of using clientless device type parameter in pass metrics](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br>**Note**: the device_info will replace this parameter. |
| _deviceUser_ | The device user identifier. |
| _appId_ | The application id/name. </br>**Note**: the device_info replaces this parameter. |

{style="table-layout:auto"}


>[!CAUTION]
>
>**Streaming Device IP Address**
></br>
>For Client-to-Server implementations, the Streaming Device IP Address is implicitly sent with this call.  For Server-to-Server implementations, where the **regcode** call is made be the Programmer Service and not the Streaming Device, the following header is required to pass the Streaming Device IP Address:
>
>
>```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>where `<streaming\_device\_ip>` is the Streaming Device public IP address. 
></br></br>
>Example :</br>
>
>```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1</br>X-Forwarded-For:203.45.101.20
>```
>
</br>

### Response XML Schema {#xml-schema}


#### Registration Code XSD {#registration-code-xsd}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>

```

 </br>

| Element Name    | Description                                                                          |
| --------------- | ------------------------------------------------------------------------------------ |
| id              | UUID generated by Registration Code Service                                          |
| code            | Registration Code generated by Registration Code Service                             |
| requestor       | Requestor ID                                                                         |
| mvpd            | Mvpd ID                                                                              |
| generated       | Registration Code creation timestamp (in milliseconds since Jan 1 1970 GMT)          |
| expires         | Timestamp when the registration code expires ((in milliseconds since Jan 1 1970 GMT) |
| deviceId        | Unique Device ID (or XSTS token)                                                     |
| deviceType      | Device Type                                                                          |
| deviceUser      | User logged-in to the device                                                         |
| appId           | Application Id                                                                       |
| appVersion      | Application Version                                                                  |
| registrationURL | URL to the Login Web App to be displayed to the end user                             |

{style="table-layout:auto"}


</br>

### Error Message XSD  {#error-message}

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="rest.pass.adobe.com"
               targetNamespace="rest.pass.adobe.com"
               attributeFormDefault="unqualified"
               elementFormDefault="unqualified">
        <xs:element name="error">
            <xs:complexType>
                <xs:all>
                    <xs:element name="status" type="xs:int" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="message" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="details" type="xs:string" minOccurs="0" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
    </xs:schema>

```
 

### Sample Response {#sample-response}

**XML:**

```XML

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```
 
**JSON:**

```JSON

    {
        "id": "678f9fea-9d364b29-246c-488f-b97e-298566d1b9e0",
        "code": "D4BDU2W",
        "requestor": "sampleRequestorId",
        "mvpd": "sampleMvpdId",
        "generated": 1348039555877,
        "expires": 1348043155877,
        "info": {
            "deviceId": "dGhpc0l.kQUR1bW15RGV2.aWNlSWQ=",
            "deviceType": "xboxOne",
            "deviceUser": "JD",
            "appId": "2345",
            "appVersion": "2.0",
            "registrationURL": "http://loginwebapp.com"
        }
    }

```
