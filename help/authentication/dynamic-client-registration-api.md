---
title: Dynamic Client Registration API
description: Dynamic Client Registration API
exl-id: 06a76c71-bb19-4115-84bc-3d86ebcb60f3
---
# Dynamic Client Registration API {#dynamic-client-registration-api}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

Currently, there are two ways in which Adobe Pass Authentication identifies and registers applications:

* browser-based clients are registered via allowed [domain listing](/help/authentication/programmer-overview.md)
* native application clients, such as iOS and Android applications are registered through signed requestor mechanism.

Adobe Pass Authentication proposes a new mechanism for registering applications. This mechanism is described in the following paragraphs.

## The Application Registration Mechanism {#appRegistrationMechanism}

### Technical Reasons {#reasons}

The authentication mechanism in Adobe Pass Authentication was relying on session cookies, but because of [Android Chrome Custom Tabs](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}, this goal cannot be achieved anymore.

Given these limitations, Adobe introduces a new registration mechanism for all its clients. It is based on the OAuth 2.0 RFC and consists
of the following steps:

1. Retrieving the software statement from TVE
Dashboard
1. Obtaining client credentials
1. Obtaining access token

### Retrieving Software Statement from TVE Dashboard {#softwareStatement}

For each application you release, you need to obtain a software statement. All software statements are provided through the TVE Dashboard, once applications are created. The software statement should be deployed together with the application on the user's device.

>[!IMPORTANT]
>
>When using a software statement, the signed requestor id mechanism won't be needed anymore.

For more details on how to create software statements, visit [Client Registration in TVE Dashboard](/help/authentication/dynamic-client-registration.md).

### Obtaining Client Credentials {#clientCredentials}

After retrieving a software statement from TVE Dashboard, you need to register your application with the Adobe Pass authorization server. Do this by performing a /register call and retrieving your unique client identifier.

**Request**

| HTTP call |                    |
|-----------|--------------------|
| path      | /o/client/register |
| method    | POST               |

| fields             |                                                                           |           |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | The software statement created in TVE Dashboard.                          | mandatory |
| redirect_uri       | The URI that the application uses for completing the authentication flow. | optional  |

| request headers |                                                                                |           |
|-----------------|--------------------------------------------------------------------------------|-----------|
| Content-Type    | application/json                                                               | mandatory |
| X-Device-Info   | The device information as defined in Passing Device and Connection Information | mandatory |
| User-Agent      | The user agent                                                                 | mandatory |

**Response**

| response headers |                  |           |
|------------------|------------------|-----------|
| Content-Type     | application/json | mandatory |

| response fields     |                 |                            |
|---------------------|-----------------|----------------------------|
| client_id           | String          | mandatory                  |
| client_secret       | String          | mandatory                  |
| client_id_issued_at | long            | mandatory                  |
| redirect_uris       | list of Strings | mandatory                  |
| grant_types         | list of Strings<br/> **accepted value**<br/> `client_credentials`: Used by insecure clients, such as Android SDK. | mandatory                  |
| error               |         **accepted values**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul>        | mandatory in an error flow |


#### Error Response {#error-response}

In case of an error, the registration server responds with an HTTP 400 (Bad Request) status code and includes the following parameters within the response:

| status code | response body | description |
| --- | --- | --- |
| HTTP 400 | {"error": "invalid_request"} | The request is missing a required parameter, includes an unsupported parameter value, repeats a parameter or it is otherwise malformed. |
| HTTP 400 | {"error": "invalid_redirect_uri"} | The redirect_uri is not allowed for this client based on its registered application. |
| HTTP 400 | {"error": "invalid_software_statement"} | The software statement is not valid. |
| HTTP 400 | {"error": "unapproved_software_statement"} | The software_id is not found in the configuration. |

#### Client Credentials Example {#client-credentials-example}

**Request:**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**Response:**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**Error response:**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### Obtaining Access Token {#accessToken}

After retrieving the unique client identifier (client id and client secret) for your application, you need to obtain an access token. The access token is a mandatory OAuth 2.0 token, used to call the Adobe Pass Authentication APIs.

>[!NOTE]
>
>Currently, access tokens have a 24 hours time to live.

**Request**


| **HTTP call** | |
| --- | --- |
| path | `/o/client/token` |
| method | POST | 

|**request parameters** | |
| --- | --- |
| `grant_type` | Received in the client registration process.<br/> **Accepted value**<br/>`client_credentials`: Used for insecure clients, such as the Android SDK. |
| `client_id` | Client identifier obtained in the client registration process. |
| `client_secret` | Client identifier obtained in the client registration process. |

**Response**

| response fields | | |
| --- | --- | --- |
| `access_token` | The access token value you should use to call the Adobe Pass APIs | mandatory |
| `expires_in` | The time in seconds until the access_token expires | mandatory |
| `token_type` | The type of the token **bearer** | mandatory |
| `created_at` | The issue time of the token | mandatory |
| **response headers** | | |
| `Content-Type` | application/json | mandatory |

**Error Response**

In case of an error, the authorization server responds with an HTTP 400 (Bad Request) status code and includes the following parameters within the response:

| status code | response body | description |
| --- | --- | --- |
| HTTP 400 | {"error": "invalid_request"} | The request is missing a required parameter, includes an unsupported parameter value (other than grant type), repeats a parameter, includes multiple credentials, utilizes more than one mechanism for authenticating the client, or is otherwise malformed. |
| HTTP 400 | {"error": "invalid_client"} | Client authentication failed because the client was unknown. The SDK MUST register with the authorization server again. |
| HTTP 400 | {"error": "unauthorized_client"} | The authenticated client is not authorized to use this authorization grant type. |

#### Obtaining Access Token Example: {#obt-access-token}

**Request:**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**Response:**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**Error response:**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## Performing Authentication Requests {#autheticationRequests}

Use the access token to perform Adobe Pass [Authentication API calls](/help/authentication/initiate-authentication.md). In order to do this, the access token needs to be added to the API request, in one of the following ways:

* by adding a new query parameter to the request. That new parameter is called **access_token**.

* by adding a new HTTP header to the request: Authorization: Bearer. We recommend you to use the HTTP header, as query strings tend to be visible in server logs.

In case of an error, the following error responses could be returned:

|     Error responses            |     |                                                                                                        |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | The request is malformed.                                                                              |
| invalid_client  | 403 | The client id is not longer permitted to perform requests. New client credentials should be generated. |
| access_denied   | 401 | The access_token is not valid (expired or invalid). The client MUST request a new access_token.        |

### Performing Authentication Requests Examples:

**Sending access token as request parameter:**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**Sending access token as HTTP header:**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**Error responses as response body:**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**Error responses as URL parameters:**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
