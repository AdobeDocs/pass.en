---
title: Adobe Single Sign-On Service
description: Learn about the Adobe Pass SSO Service that enables seamless authentication across multiple devices and applications.
exl-id: a1ff85d4-f7d2-4dea-b82f-d29730d9012f
---

# Adobe Single Sign-On Service {#sso-service}

This document describes use cases, endpoints and API for Adobe Single Sign-On Service.

**Current Revision - 1.0.0**

## Scope {#scope}

Adobe Pass SSO Service enables seamless authentication across multiple devices and applications, providing a unified user experience while maintaining security and compliance standards. This service addresses the growing need for cross-platform authentication in today's multi-device streaming landscape.

## Overview {#overview}

### What it is {#what-it-is}

A comprehensive Single Sign-On solution that allows users to authenticate once and manage the transfer of authentication in an informed way to other devices

### Current challenges for authentication {#current-challenges}

* User must authenticate with every streaming service he has a subscription to
* User must authenticate separately on each device or application
* Due to difficulty typing a password in authentication flow on some platforms, this may lead to increased abandonment rates

### Opportunity for an Adobe Pass SSO Service {#opportunity}

* Increasing number of streaming services requiring their own authentication
* Growing demand for seamless cross-device experiences
* Increasing number of streaming devices per household
* Need for unified authentication per household

### Business Benefits {#business-benefits}

#### Content Providers {#content-providers}

* **Increased User Engagement** - Seamless experience leads to longer session times
* **Reduced Friction** - Lower authentication barriers increase content consumption
* **Improved Retention** - Better user experience reduces churn
* **Cost Reduction** - Fewer support tickets related to authentication issues

#### End Users {#end-users}

* **Seamless Experience** - Authenticate once, access everywhere
* **Time Savings** - No repeated login processes
* **Device Flexibility** - Switch between devices without interruption
* **Consistent Experience** - Uniform authentication across all platforms

#### IdPs (MVPDs, Telcos, etc) {#idps}

* MVPDs can be informed of additional devices using an authenticated SSO
* **Enhanced User Satisfaction** - Improved authentication experience
* **Reduced Support Load** - Fewer authentication-related support calls
* **Competitive Advantage** - Better user experience than competitors

## Use Cases {#use-cases}

### Identity mapping {#identity-mapping}

The service builds the ability to link a D2C and a TVE account in the same app.

More streaming services are building bundles to be sold to a third party (MVPD/virtual MVPD/Telco, etc.). Users may end up having to handle multiple accounts in the same app. To create a seamless authentication experience, a service needs to bridge these accounts to simplify the login experience.

User will authenticate with their D2C account, then authenticate ONCE with a different account (ex. MVPD). With our service, these accounts will be linked, which means that going forward, subsequent authentications on different devices can be done only with the D2C account.

### Cross-Device SSO {#cross-device-sso}

Authentication on a TV-connected device can be more cumbersome than on a mobile phone. A good user experience would be to authenticate on the phone and then pass that authentication on to the smart TV.

## Key Components {#key-components}

* **Service Token API** - key component that manages securely the Single Sign On mechanism
* **List API** - Application can help the user understand the list of devices in its ecosystem
* **Link API** - Application enable the user to add additional devices in its ecosystem
* **Unlink API** - Application enable the user to remove devices in its ecosystem

## Use Cases Detailed {#use-cases-detailed}

### D2C-TVE SSO {#d2c-tve-sso}

This use case enables linking between D2C and TVE(MVPD) credentials on one device and leveraging that linked profile on other devices within the same application.

![D2C-TVE SSO Flow](../../../assets/sso_service_d2c_1.png)

![Cross-Device SSO Flow](../../../assets/sso_service_d2c_2.png)

### Cross-Device SSO {#cross-device-sso-detailed}

This use case enables users that already authenticated on one device to reuse the authenticated profile on the same D2C or TVE application installed on other devices (application required to implement Adobe Pass REST V2 for authentication and authorization).

## How to integrate Adobe SSO Service in a D2C-TVE application {#integration}

### Step 1 - Get a common identifier {#step-1}

To integrate Adobe SSO Service, an application implementation should establish an unique and persistent ID to use as common identifier SSO attribute in X-SSO-ID. This can be obtained by authenticating a user with a D2C service and retain an attribute about this authentication.

### Step 2 - Obtain a Service Token {#step-2}

Using the common identifier in X-SSO-ID in POST /serviceToken endpoint will retrieve a signed JWT with the following payload:

```json
{
  "iss": "ssoservicetoken",
  "sub": "unique_common_identifier",
  "nbf": 1758093558,
  "exp": 1758097158,
  "iat": 1758093558
}
```

The Service Token has "iat" - issued at and "exp" - expiration time in which interval the Service Token is valid. In case of expiration, a new JWT can be obtain using GET /serviceToken endpoint with the expired Service Token.

### Step 3 - Authenticate using Adobe Pass REST API V2 with a TVE MVPD {#step-3}

The authentication with Adobe Pass should be implemented using the Service Token: [REST API V2 - Single Sign-On Service Token Flows](https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-flows/rest-api-v2-single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows)

### Step 4 - Link another device {#step-4}

From the authenticated application, a link can be created to be used on a different device using /link API

```json
{
    "status": "CREATED",
    "code": "228128",
    "notBefore": 1758094617220,
    "notAfter": 1758098217220
}
```

The "code" is a short lived link code in a form of a sequence of 6 digits that the user will introduce in an unauthenticated application on a secondary device

### Step 5 - Retrieve Single Sign On authentication {#step-5}

On a different device, once the user introduced the code, the application can:

* retrieve identity from the D2C Service
* retrieve MVPD profile from Adobe Pass with REST V2 API

The MVPD profile will be valid thru SSO for the period the initial authentication was obtained.

In case MVPD invalidates the profile or the user choose to logout from MVPD, the application using Adobe Pass REST API V2 would no longer have a profile record and should require the user to authenticate again with the MVPD.

### Step 6 - Manage Single Sign On on other devices {#step-6}

An application can get information about all other devices linked with the same common identifier using /list API.

At any time, a device can be removed from the Single Sign On by unlinking that device with /unlink API.

## APIs {#apis}

### Service Token API {#service-token-api}

#### Description {#service-token-description}

The Service Token API can be used to request and manage service tokens that enable Single Sign-On (SSO) functionality between multiple applications or devices. These service tokens identify authenticated profiles (SSO profiles) and are essential for establishing and maintaining SSO connections.

>[!WARNING]
>
>Service tokens contain sensitive authentication information. Applications must handle these tokens securely and never expose them to untrusted parties.

The Service Token API provides two primary endpoints:

* **POST /api/{serviceProvider}/serviceToken** - Obtain a newly created JWS service token
* **GET /api/{serviceProvider}/serviceToken** - Refresh an existing JWS service token

In case the Service Token API request could not be serviced due to an Adobe Pass Authentication services error, additional error information will be included as part of the API response.

#### POST - serviceToken {#post-service-token}

##### Request {#post-service-token-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/{serviceProvider}/serviceToken</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>POST</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Path Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">serviceProvider</td>
      <td>The service provider identifier for which the token is being requested.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-authorization">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Device-Identifier</td>
      <td>
         The generation of the device identifier payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-ap-device-identifier">AP-Device-Identifier</a> header documentation.
         <br/><br/>
         This identifier is used as the default SSO identifier when X-SSO-ID is not provided.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">X-Device-Info</td>
      <td>
         The device information as specified in <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-x-device-info">X-Device-Info</a> header documentation.
         <br/><br/>
         <b>Strongly recommended</b> to use when the application's device platform allows providing valid values explicitly.
         <br/><br/>
         The Adobe Pass Authentication backend will merge explicitly set values with implicitly extracted values. When not provided, default extracted values will be used.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">X-SSO-LINK</td>
      <td>
         The link code that associates this request with an existing authenticated profile. When provided, the response will include a service token for SSO with the profile that generated the link code.
         <br/><br/>
         This is typically used when a secondary application or device wants to connect to an authenticated profile from a primary application or device.
      </td>
      <td>required if x-sso-id is not provided</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">X-SSO-ID</td>
      <td>
         The common identifier that the application requests to base SSO on.
         <br/><br/>
         When provided, this identifier will be used to establish a common SSO profile across devices and/or applications.
      </td>
      <td>required if x-sso-link is not provided</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified it must be application/json.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

##### Response {#post-service-token-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>201</td>
      <td>Created</td>
      <td>
        The service token was successfully generated and returned in the response body.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

###### Success {#success-post-service-token}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>201</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">status</td>
      <td>HTTP status (e.g., "CREATED")</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">jws</td>
      <td>A Base64-encoded JSON Web Signature (JWS) containing the service token. This token can be used in subsequent API calls to identify the authenticated profile and enable SSO functionality.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notBefore</td>
      <td>Epoch ms, or 0 on error</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notAfter</td>
      <td>Epoch ms, or 0 on error</td>
      <td><i>required</i></td>
   </tr>
</table>

###### Error {#error-post-service-token}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>400, 401, 500</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"></td>
      <td>The response body may provide additional error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples-post-service-token}

### 1. Request a new service token (with SSO ID)

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/{serviceProvider}/serviceToken HTTP/1.1

    Authorization: Bearer <access_token>
    X-SSO-ID: <sso_id>
    AP-Device-Identifier: fingerprint <base64_device_id>
    X-Device-Info: <base64_device_info>
    Accept: application/json
```

>[!TAB Response]

```HTTPS
HTTP/1.1 201 Created

Content-Type: application/json

{
  "status": "CREATED",
  "serviceToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "notBefore": 1710000000000,
  "notAfter": 1710003600000
}
```

>[!ENDTABS]

### 2. Request a new service token (with SSO Link)

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/{serviceProvider}/serviceToken HTTP/1.1

    Authorization: Bearer <access_token>
    X-SSO-LINK: <link_code>
    AP-Device-Identifier: fingerprint <base64_device_id>
    X-Device-Info: <base64_device_info>
    User-Agent: <user_agent>
    Accept: application/json
```

>[!TAB Response]

```HTTPS
HTTP/1.1 201 Created

Content-Type: application/json

{
  "status": "CREATED",
  "serviceToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "notBefore": 1710000000000,
  "notAfter": 1710003600000
}
```

>[!ENDTABS]

#### GET - serviceToken {#get-service-token}

##### Request {#get-service-token-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/{serviceProvider}/serviceToken</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>GET</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Path Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">serviceProvider</td>
      <td>The service provider identifier for which the token is being requested.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-authorization">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AD-Service-Token</td>
      <td>
         A previously obtained service token that needs to be refreshed.
         <br/><br/>
         This token must be valid or have expired recently to be eligible for refresh.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified it must be application/json.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

##### Response {#get-service-token-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>200</td>
      <td>OK</td>
      <td>
        The service token was successfully refreshed and returned in the response body.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token or service token is invalid, the client needs to obtain a new access token or service token and try again. For more details refer to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

###### Success {#success-get-service-token}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>200</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">status</td>
      <td>HTTP status (e.g., "OK")</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">jws</td>
      <td>A Base64-encoded JSON Web Signature (JWS) containing the refreshed service token. This token can be used in subsequent API calls to identify the authenticated profile and enable SSO functionality.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notBefore</td>
      <td>Epoch ms, or 0 on error</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notAfter</td>
      <td>Epoch ms, or 0 on error</td>
      <td><i>required</i></td>
   </tr>
</table>

###### Error {#error-get-service-token}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>400, 401, 500</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"></td>
      <td>The response body may provide additional error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples-get-service-token}

### 1. Request to refresh a service token

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/{serviceProvider}/serviceToken HTTP/1.1

    Authorization: Bearer <access_token>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json

{
  "status": "OK",
  "serviceToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "notBefore": 1710000000000,
  "notAfter": 1710003600000
}
```

>[!ENDTABS]

### Link API {#link-api}

#### Description {#link-description}

The Link API can be used to request a link code (or QR code) that can enable Single Sign-On (SSO) between multiple applications or devices. This link code allows users to connect a new application or device to an existing authenticated profile (SSO profile), providing a seamless SSO experience across applications or devices.

The Link API requires a valid service token to be provided in the AD-Service-Token header.

The generated link code is typically displayed to users on a primary application or device and entered on a secondary application or device to establish the SSO connection. The link code has a limited validity period (typically 5-30 minutes) and is meant for one-time use.

In case the Link API request could not be serviced due to an Adobe Pass Authentication services error, then additional error information will be included as part of the Link API response result.

#### POST - link {#post-link}

##### Request {#post-link-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/{serviceProvider}/link</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>POST</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Path Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">serviceProvider</td>
      <td>The service provider identifier for which the token is being requested.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-authorization">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Device-Identifier</td>
      <td>The generation of the device identifier payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-ap-device-identifier">AP-Device-Identifier</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AD-Service-Token</td>
      <td>
         The generation of the service token is described by the Service Token API documentation.
         <br/><br/>
         This service token identifies the authenticated profile for which the link code will be generated.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified it must be application/json.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

##### Response {#post-link-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>201</td>
      <td>Created</td>
      <td>
        The link code was successfully generated and returned in the response body.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

###### Success {#success-post-link}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>201</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">status</td>
      <td>HTTP status (e.g., "CREATED")</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">link</td>
      <td>A short numeric or alphanumeric code that can be used on a secondary application or device to establish an SSO connection.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notBefore</td>
      <td>The timestamp (in milliseconds since epoch) when the link code becomes valid.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">notAfter</td>
      <td>The timestamp (in milliseconds since epoch) when the link code expires.</td>
      <td><i>required</i></td>
   </tr>
</table>

###### Error {#error-post-link}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>400, 401, 500</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"></td>
      <td>The response body may provide additional error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples-post-link}

### 1. Request a link code for an existing authenticated profile

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/{serviceProvider}/link HTTP/1.1

    Authorization: Bearer <access_token>
    AP-Device-Identifier: fingerprint <base64_device_id>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
```

>[!TAB Response]

```HTTPS
HTTP/1.1 201 Created

Content-Type: application/json

{            
   "status": "CREATED",
   "code": "123456",
   "notBefore": 1623840000000,
   "notAfter": 1623842700000
}
```

>[!ENDTABS]

### Unlink API {#unlink-api}

#### Description {#unlink-description}

The Unlink API can be used to request the removal of a device or multiple devices from an authenticated profile (SSO profile). This API allows users to disconnect devices from their SSO setup, providing control over which devices have access to their authenticated profile.

>[!WARNING]
>
>The Unlink API requires a valid service token to be provided in the AD-Service-Token header.

In case the Unlink API request could not be serviced due to an Adobe Pass Authentication services error, then additional error information will be included as part of the Unlink API response result.

#### POST - unlink {#post-unlink}

##### Request {#post-unlink-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/{serviceProvider}/unlink</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>POST</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Path Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">serviceProvider</td>
      <td>The service provider identifier.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">devices</td>
      <td>
         Array of device identifiers to unlink.
         <br/><br/>
         Example:<br/><code>["deviceid1", "deviceid2", "deviceid3"]</code>
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-authorization">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>
         The accepted media type for the resources being sent.
         <br/><br/>
         It must be application/json.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Device-Identifier</td>
      <td>The generation of the device identifier payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-ap-device-identifier">AP-Device-Identifier</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AD-Service-Token</td>
      <td>
         The generation of the service token is described by the Service Token API documentation.
         <br/><br/>
         This service token identifies the authenticated profile for which devices will be unlinked.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified it must be application/json.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

##### Response {#post-unlink-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>200</td>
      <td>OK</td>
      <td>
        The requested device(s) have been successfully unlinked from the SSO setup.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>405</td>
      <td>Method Not Allowed</td>
      <td>
        The HTTP method is invalid, the client needs to use an HTTP method that is permitted for the requested resource and try again.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

###### Success {#success-post-unlink}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>200</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">status</td>
      <td>Information on operation result: "OK"</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">unlinkedDevices</td>
      <td>
         List of successfully unlinked devices.
         <br/><br/>
         Example:<br/><code>["deviceid1", "deviceid2", "deviceid3"]</code>
      </td>
      <td><i>required</i></td>
   </tr>
</table>

###### Error {#error-post-unlink}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>400, 401, 405, 500</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"></td>
      <td>The response body may provide additional error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples-post-unlink}

### 1. Request to unlink devices from an SSO profile

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/{serviceProvider}/unlink HTTP/1.1

    Authorization: Bearer <access_token>
    Content-Type: application/json
    AP-Device-Identifier: fingerprint <base64_device_id>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
    
{
  "devices": [
    "deviceid1",
    "deviceid2",
    "deviceid3"
  ]
}
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json

{
  "status": "OK",
  "unlinkedDevices": [
    "deviceid1",
    "deviceid2",
    "deviceid3"
  ]
}
```

>[!ENDTABS]

### 2. Request to unlink devices with partial success

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/{serviceProvider}/unlink HTTP/1.1

    Authorization: Bearer <access_token>
    Content-Type: application/json
    AP-Device-Identifier: fingerprint <base64_device_id>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
    
{
  "devices": [
    "deviceid1",
    "unknowndevice",
    "deviceid3"
  ]
}
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json

{
  "status": "OK",
  "unlinkedDevices": [
    "deviceid1",
    "deviceid3"
  ]
}
```

>[!ENDTABS]

### List API {#list-api}

#### Description {#list-description}

The List API can be used to obtain a list of devices currently connected to an authenticated profile (SSO profile). This API allows users and applications to view which devices are part of their SSO setup, providing visibility and management capabilities for their authenticated experience across multiple devices.

>[!WARNING]
>
>The List API requires a valid service token to be provided in the AD-Service-Token header.

The List API returns details about each device in the authenticated profile (SSO profile), including device identifiers and metadata that may help users recognize their devices. This information can be used to help users make informed decisions about which devices should remain in their SSO setup.

In case the List API request could not be serviced due to an Adobe Pass Authentication services error, then additional error information will be included as part of the List API response result.

#### GET - list {#get-list}

##### Request {#get-list-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/{serviceProvider}/list</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>GET</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Path Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">serviceProvider</td>
      <td>The service provider identifier.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-authorization">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Device-Identifier</td>
      <td>The generation of the device identifier payload is described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-ap-device-identifier">AP-Device-Identifier</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AD-Service-Token</td>
      <td>
         The generation of the service token is described by the Service Token API documentation.
         <br/><br/>
         This service token identifies the authenticated profile for which the device list will be retrieved.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified it must be application/json.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

##### Response {#get-list-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>200</td>
      <td>OK</td>
      <td>
        The list of devices in the SSO setup was successfully retrieved and returned in the response body.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>405</td>
      <td>Method Not Allowed</td>
      <td>
        The HTTP method is invalid, the client needs to use an HTTP method that is permitted for the requested resource and try again.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

###### Success {#success-get-list}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>200</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">devices</td>
      <td>
         JSON containing a map of key, value pairs.
         <br/><br/>
         <b>Key:</b> deviceId - The device identifier payload as described in the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-appendix/rest-api-v2-appendix-headers/rest-api-v2-appendix-headers-ap-device-identifier">AP-Device-Identifier</a> header documentation
         <br/><br/>
         <b>Value:</b> attributes - JSON containing a map of device metadata attributes including:
         <ul>
            <li>device type</li>
            <li>platform</li>
            <li>user agent</li>
            <li>other relevant metadata that helps identify the device</li>
         </ul>
         The values for the attributes can be simple (string, integer, boolean, etc.)
      </td>
      <td><i>required</i></td>
   </tr>
</table>

###### Error {#error-get-list}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Status</td>
      <td>400, 401, 405, 500</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>application/json</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"></td>
      <td>The response body may provide additional error information that adheres to the <a href="https://experienceleague.adobe.com/en/docs/pass/authentication/integration-guide-programmers/standard-features/error-reporting/enhanced-error-codes">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples-get-list}

### 1. Request to list devices in an SSO profile

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/{serviceProvider}/list HTTP/1.1

    Authorization: Bearer <access_token>
    AP-Device-Identifier: fingerprint <base64_device_id>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json

{
  "devices": {
    "deviceid1": {
      "deviceType": "smartTV",
      "model": "Samsung",
      "os": "Tizen",
      "osVersion": "5.0",
      "lastSeen": 1623840000000,
      "type": "regular"
    },
    "deviceid2": {
      "deviceType": "mobile",
      "model": "iPhone",
      "os": "iOS",
      "osVersion": "14.5",
      "lastSeen": 1623830000000,
      "type": "sso"
    },
    "deviceid3": {
      "deviceType": "tablet",
      "model": "iPad",
      "os": "iPadOS",
      "osVersion": "14.5",
      "lastSeen": 1623820000000,
      "type": "sso"
    }
  }
}
```

>[!ENDTABS]

### 2. Request to list devices with no linked devices

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/{serviceProvider}/list HTTP/1.1

    Authorization: Bearer <access_token>
    AP-Device-Identifier: fingerprint <base64_device_id>
    AD-Service-Token: <service_token>
    Accept: application/json
    User-Agent: <user_agent>
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json

{
  "devices": {}
}
```

>[!ENDTABS]

## Error Codes {#error-codes}

### Error Response Structure {#error-structure}

All error responses include these fields:

| Field | Type | Description |
|:---|:---|:---|
| status | Integer | HTTP status code (400, 401, 500, etc.) |
| code | String | Machine-readable error code |
| message | String | Human-readable description |
| action | String | Suggested action for client |
| helpUrl | String | Documentation link |
| trace | String | Unique request ID (UUID) for correlation |

**Error Response Example**

```json
{
  "status": "BAD_REQUEST",
  "error": {
    "status": 400,
    "code": "header_missing",
    "message": "Required header is missing",
    "action": "check_headers",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "trace": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
  }
}
```

**Success Response Example**

```json
{
  "status": "OK",
  "serviceToken": "eyJhbGciOiJIUzI1NiIs...",
  "notBefore": 1697500800000,
  "notAfter": 1697587200000
}
```

>[!NOTE]
>
>Success responses do NOT include an error field. Error responses do NOT include success fields.

### Error Codes Catalog {#error-catalog}

#### General Errors

| code | status | message | action |
|:---|:---|:---|:---|
| token_invalid | 400 | The provided token is invalid | get_new_token |
| token_expired | 401 | The token has expired | get_new_token |
| header_missing | 400 | A required header is missing | check_headers |
| unauthorized | 401 | Unauthorized access | none |
| internal_error | 500 | An internal error occurred | none |

#### Validation Errors

| code | status | message | action |
|:---|:---|:---|:---|
| request_null | 400 | Request object cannot be null | none |

#### POST ServiceToken Errors

| code | status | message | action |
|:---|:---|:---|:---|
| header_missing | 400 | Either x-sso-id or x-sso-link header is required for POST requests | check_headers |
| header_missing | 400 | AP-Device-Identifier header is required for POST requests | check_headers |

#### GET ServiceToken Errors

| code | status | message | action |
|:---|:---|:---|:---|
| header_missing | 400 | AD-Service-Token header is required for GET requests | check_headers |
| header_invalid | 401 | Invalid JWT signature in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error validating JWT signature | get_new_token |
| header_invalid | 401 | JWT subject (sub) is missing or empty in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error extracting JWT subject | get_new_token |

#### Link Validation Errors

| code | status | message | action |
|:---|:---|:---|:---|
| header_missing | 401 | AD-Service-Token header is required for link requests | check_headers |
| header_invalid | 401 | Invalid JWT signature in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error validating JWT signature | get_new_token |

#### Unlink Validation Errors

| code | status | message | action |
|:---|:---|:---|:---|
| header_missing | 401 | AD-Service-Token header is required for unlink requests | check_headers |
| header_invalid | 401 | Invalid JWT signature in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error validating JWT signature | get_new_token |
| header_invalid | 401 | JWT subject (sub) is missing or empty in AD-Service-Token | get_new_token |
| request_invalid | 400 | Devices list cannot be null or empty | check_request_body |

#### List Validation Errors

| code | status | message | action |
|:---|:---|:---|:---|
| header_missing | 401 | AD-Service-Token header is required for list requests | check_headers |
| header_invalid | 401 | Invalid JWT signature in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error validating JWT signature | get_new_token |
| header_invalid | 401 | JWT subject (sub) is missing or empty in AD-Service-Token | get_new_token |
| header_invalid | 401 | Error extracting JWT subject | get_new_token |

