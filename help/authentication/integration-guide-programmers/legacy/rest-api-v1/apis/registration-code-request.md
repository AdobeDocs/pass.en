---
title: Registration Page
description: Registration Page
exl-id: 581b8e2e-7420-4511-88b9-f2cd43a41e10
---
# (Legacy) Registration Page {#registration-page}

## REST API Endpoints {#clientless-endpoints}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md)

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<br>

## Description {#create-reg-code-svc}

Returns randomly generated registration Code and Login Page URI.

| Endpoint | Called  <br>By | Input   <br>Parameter | HTTP  <br>Method | Response | HTTP  <br>Response |
| --- | --- | --- | --- | --- | --- |
| <REGGIE_FQDN>/reggie/v1/{requestor}/regcode<br>For example:<br>REGGIE_FQDN/reggie/v1/sampleRequestorId/regcode | Streaming App<br>or<br>Programmer Service | 1.  requestor  <br>    (Path component)<br>2.  deviceId (Hashed)   <br>    (Mandatory)<br>3.  device_info/X-Device-Info (Mandatory)<br>4.  mvpd (Optional)<br>5.  ttl (Optional)<br> | POST | XML or JSON containing a registration code and information or error details if unsuccessful. See samples below. | 201 |

{style="table-layout:auto"}

| Input Parameter | Type                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                        |
| --- |------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | Header <br> Value: Bearer <access_token> | DCR Access Token                                                    |
| Accept | Header <br> Value: application/json      | indicate which content type the client should be able to understand |
| requestor | Query Parameter                          | The Programmer requestorId for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                      |
| deviceId | Query Parameter                          | The device id bytes.                                                                                                                                                                                                                                                                                                                                                                                               |
| device_info/<br>X-Device-Info | device_info: Body <br> X-Device-Info: Header | Streaming Device information.<br>**Note**: This MAY be passed device_info as a URL paramater, but due to the potential size of this paramater and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. <br>See the full details in [Passing Device and Connection Information](/help/authentication/integration-guide-programmers/legacy/client-information/passing-client-information-device-connection-and-application.md). |
| mvpd | Query Parameter                          | The MVPD ID for which this operation is valid.                                                                                                                                                                                                                                                                                                                                                                     |
| ttl | Query Parameter                          | How long this regcode should live in seconds.<br>**Note**: The maximum value allowed for ttl is 36000 seconds (10 hours). Higher values result in a 400 HTTP response (bad request). If `ttl` is left empty, Adobe Pass Authentication sets a default value of 30 minutes.                                                                                                                                        |
| _deviceType_ | Query Parameter                          | Deprecated, should not be used.                                                                                                                                                                                                                                                                                                                                                                                    |         
| _deviceUser_ | Query Parameter                          | Deprecated, should not be used.                                                                                                                                                                                                                                                                                                                                                                                    |
| _appId_ | Query Parameter                          | Deprecated, should not be used.                                                                                                                                                                                                                                                                                                                                                                                    |

{style="table-layout:auto"}

>[!CAUTION]
>
>**Streaming Device IP Address**
><br>
>For Client-to-Server implementations, the Streaming Device IP Address is implicitly sent with this call.  For Server-to-Server implementations, where the **regcode** call is made be the Programmer Service and not the Streaming Device, the following header is required to pass the Streaming Device IP Address:
>
>
>```
>X-Forwarded-For : <streaming_device_ip> 
>```
>
>where `<streaming\_device\_ip>` is the Streaming Device public IP address. 
><br><br>
>Example :<br>
>
>```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1<br>X-Forwarded-For:203.45.101.20
>```
>
<br>

### Response JSON


#### Registration Code JSON SAMPLES

```JSON
{
  "id": "ef5a79e8-7c8a-41d6-a45a-e378c6c7c8b5",
  "code": "IYQD5JQ",
  "requestor": "sampleRequestorId",
  "mvpd": "sampleMvpdId",
  "generated": 1704963921144,
  "expires": 1704965721144,
  "info": {
    "deviceId": "c28tZGV2aWQtMDAz",
    "deviceInfo": "eyJ0eXBlIjoiU2V0VG9wQm94IiwibW9kZWwiOiJBRlRNTSIsInZlcnNpb24iOnsibWFqb3IiOjAsIm1pbm9yIjowLCJwYXRjaCI6MCwicHJvZmlsZSI6IiJ9LCJoYXJkd2FyZSI6eyJuYW1lIjoiQUZUTU0iLCJ2ZW5kb3IiOiJVbmtub3duIiwidmVyc2lvbiI6eyJtYWpvciI6MCwibWlub3IiOjAsInBhdGNoIjowLCJwcm9maWxlIjoiIn0sIm1hbnVmYWN0dXJlciI6IlJva3UifSwib3BlcmF0aW5nU3lzdGVtIjp7Im5hbWUiOiJBbmRyb2lkIiwiZmFtaWx5IjoiQW5kcm9pZCIsInZlbmRvciI6IkFtYXpvbiIsInZlcnNpb24iOnsibWFqb3IiOjcsIm1pbm9yIjoxLCJwYXRjaCI6MiwicHJvZmlsZSI6IiJ9fSwiYnJvd3NlciI6eyJuYW1lIjoiQ2hyb21lIiwidmVuZG9yIjoiR29vZ2xlIiwidmVyc2lvbiI6eyJtYWpvciI6MTEyLCJtaW5vciI6MCwicGF0Y2giOjU2MTUsInByb2ZpbGUiOiIifSwidXNlckFnZW50IjoiTW96aWxsYS81LjAgKExpbnV4OyBBbmRyb2lkIDcuMS4yOyBBRlRNTSBCdWlsZC9OUzYyOTc7IHd2KSBBcHBsZVdlYktpdC81MzcuMzYgKEtIVE1MLCBsaWtlIEdlY2tvKSBWZXJzaW9uLzQuMCBDaHJvbWUvMTEyLjAuNTYxNS4xOTcgTW9iaWxlIFNhZmFyaS81MzcuMzYgQWRvYmVQYXNzTmF0aXZlRmlyZVRWLzMuMC44Iiwib3JpZ2luYWxVc2VyQWdlbnQiOiJNb3ppbGxhLzUuMCAoTGludXg7IEFuZHJvaWQgNy4xLjI7IEFGVE1NIEJ1aWxkL05TNjI5Nzsgd3YpIEFwcGxlV2ViS2l0LzUzNy4zNiAoS0hUTUwsIGxpa2UgR2Vja28pIFZlcnNpb24vNC4wIENocm9tZS8xMTIuMC41NjE1LjE5NyBNb2JpbGUgU2FmYXJpLzUzNy4zNiBBZG9iZVBhc3NOYXRpdmVGaXJlVFYvMy4wLjgifSwiZGlzcGxheSI6eyJ3aWR0aCI6MCwiaGVpZ2h0IjowLCJwcGkiOjAsIm5hbWUiOiJESVNQTEFZIiwidmVuZG9yIjpudWxsLCJ2ZXJzaW9uIjpudWxsLCJkaWFnb25hbFNpemUiOm51bGx9LCJhcHBsaWNhdGlvbklkIjpudWxsLCJjb25uZWN0aW9uIjp7ImlwQWRkcmVzcyI6IjE5My4xMDUuMTQwLjEzMSIsInBvcnQiOiI5OTM0Iiwic2VjdXJlIjpmYWxzZSwidHlwZSI6bnVsbH19",
    "userAgent": "Mozilla/5.0 (Linux; Android 7.1.2; AFTMM Build/NS6297; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/112.0.5615.197 Mobile Safari/537.36 AdobePassNativeFireTV/3.0.8",
    "originalUserAgent": "Mozilla/5.0 (Linux; Android 7.1.2; AFTMM Build/NS6297; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/112.0.5615.197 Mobile Safari/537.36 AdobePassNativeFireTV/3.0.8",
    "authorizationType": "OAUTH2",
    "sourceApplicationInformation": {
      "id": "14138364-application-id",
      "name": "application name",
      "version": "1.0.0"
    }
  }
}
```

 <br>

| Element Name                      | Description                                                                                                      |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------|
| id                                | UUID generated by Registration Code Service                                                                      |
| code                              | Registration Code generated by Registration Code Service                                                         |
| requestor                         | Requestor ID                                                                                                     |
| mvpd                              | Mvpd ID                                                                                                          |
| generated                         | Registration Code creation timestamp (in milliseconds since Jan 1 1970 GMT)                                      |
| expires                           | Timestamp when the registration code expires ((in milliseconds since Jan 1 1970 GMT)                             |
| deviceId                          | Base64 Unique Device ID                                                                                          |
| info:deviceId                     | Base64 Device Type                                                                                               |
| info:deviceInfo                   | Base64 Normalized Device Information build on information received from User-Agent, X-Device-Info or device_info |
| info:userAgent                    | User Agent sent by the application                                                                               |
| info:originalUserAgent            | User Agent sent by the application                                                                               |
| info:authorizationType            | OAUTH2 for calls using DCR                                                                                       |
| info:sourceApplicationInformation | Application Info as configured in DCR                                                                            |

{style="table-layout:auto"}


<br>

### Error Message JSON Response Sample (#error-sample-response)

```JSON
{
  "status": 400,
  "message": "Required '<>' is not present"
}
```
 
