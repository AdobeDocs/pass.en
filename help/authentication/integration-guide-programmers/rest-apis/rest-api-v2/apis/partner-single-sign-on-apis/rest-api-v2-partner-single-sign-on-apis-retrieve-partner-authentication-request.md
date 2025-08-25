---
title: Retrieve partner authentication request
description: REST API V2 - Retrieve partner authentication request
exl-id: 52d8a8e9-c176-410f-92bc-e83449278943
---
# Retrieve partner authentication request {#retrieve-partner-authentication-request}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

## Request {#request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/v2/{serviceProvider}/sessions/sso/{partner}</td>
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
      <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
    <tr>
      <td style="background-color: #DEEBFF;">partner</td>
      <td>The name of the partner (e.g., Apple) that provides the single sign-on framework integrated with Adobe Pass Authentication flows.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">domainName</td>
      <td>
        The originating domain of the application performing MVPD login.
        <br/><br/>
        If the streaming device platform has limitations in providing a value, then an application will have to resume the authentication session and provide a valid value.
        <br/><br/>
        This will be used in case of fallback scenarios where the response indicates that the streaming application should proceed with the basic authentication flow.
      </td>
      <td><i>required</i></td>
   </tr>
    <tr>
      <td style="background-color: #DEEBFF;">redirectUrl</td>
      <td>
        The final redirect URL to which the user agent navigates when the authentication flow for the MVPD is completed.
        <br/><br/>
        The value must be URL-encoded.
        <br/><br/>
        If the streaming device platform has limitations in providing a value, then an application will have to resume the authentication session and provide a valid value.
        <br/><br/>
        This will be used in case of fallback scenarios where the response indicates that the streaming application should proceed with the basic authentication flow.
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
      <td>The generation of the bearer token payload is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-authorization.md">Authorization</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Content-Type</td>
      <td>
         The accepted media type for the resources being sent.
         <br/><br/>
         It must be application/x-www-form-urlencoded.
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Device-Identifier</td>
      <td>The generation of the device identifier payload is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md">AP-Device-Identifier</a> header documentation.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">X-Device-Info</td>
      <td>
         The generation of the device information payload is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-x-device-info.md">X-Device-Info</a> header documentation.
         <br/><br/>
         It is strongly recommended to always use it when the application's device platform allows for the explicit provision of valid values.
         <br/><br/>
         When provided, the Adobe Pass Authentication backend will merge explicitly set values with extracted values implicitly (by default).
         <br/><br/>
         When not provided, the Adobe Pass Authentication backend will use extracted values implicitly (by default).
      </td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Partner-Framework-Status</td>
      <td>
        The generation of the single sign-on payload for the Partner method is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md">AP-Partner-Framework-Status</a> header documentation.
        <br/><br/>
        For more details about single sign-on enabled flows using a partner, refer to the  <a href="../../flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-partner-flows.md">Single sign-on using partner flows</a> documentation.</td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">X-Forwarded-For</td>
      <td>
         The IP address of the streaming device.
         <br/><br/>
         It is strongly recommended to always use it for server to server implementations, particularly when the call is made by the programmer service rather than the streaming device.
         <br/><br/>
         For client to server implementations, the IP address of the streaming device is sent implicitly.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AP-Visitor-Identifier</td>
      <td>
        The generation of the visitor identifier payload  is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-ap-visitor-identifier.md">AP-Visitor-Identifier</a> header documentation.
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified, it must be application/json;charset=utf-8.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">User-Agent</td>
      <td>The user agent of the client application.</td>
      <td>optional</td>
   </tr>
</table>

## Response {#response}

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
        The response body contains information about the next actions needed to perform authentication.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="../../../../features-standard/error-reporting/enhanced-error-codes.md">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="../../../rest-api-dcr/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>405</td>
      <td>Method Not Allowed</td>
      <td>
        The HTTP method is invalid, the client needs to use an HTTP method that is permitted for the requested resource and try again. For more details refer to the <a href="#request">Request</a> section.
      </td>
   </tr>
   <tr>
      <td>500</td>
      <td>Internal Server Error</td>
      <td>
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="../../../../features-standard/error-reporting/enhanced-error-codes.md">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
</table>

### Success {#success}

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
      <td style="background-color: #DEEBFF;"></td>
      <td>
         JSON object having the following attributes:
         <table style="table-layout:auto">
            <tr>
               <th style="background-color: #EFF2F7;">Attribute</th>
               <th style="background-color: #EFF2F7"></th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">actionName</td>
               <td>
                  The action the streaming device needs to perform in order to complete the authentication flow.
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>partner_profile</b><br/>The streaming device can use the provided partner authentication request to obtain a partner authentication response that can be leveraged to retrieve a profile.</li>
                    <li><b>authenticate</b><br/>When the partner single sign-on flow cannot proceed, the streaming device can fall back to the basic authentication flow.<br/>The streaming device or another device needs to open the provided URL in a user agent.</li>
                    <li><b>resume</b><br/>When the partner single sign-on flow cannot proceed, the streaming device can fall back to the basic authentication flow.<br/>The streaming device or another device needs to provide the missing parameters and resume the authentication session using the code.</li>
                    <li><b>authorize</b><br/>The streaming device can directly proceed with decisions flows.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">actionType</td>
               <td>
                  The type of interaction the streaming device must perform in order to continue the flow with the action specified by the 'actionName' attribute.
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>interactive</b><br/>The flow continues with a navigation to the provided URL using a user agent.</li>
                    <li><b>direct</b><br/>The flow continues with a direct call to the provided URL using an HTTP client available for the client implementation.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">reasonType</td>
               <td>
                  The type of reason that explains the 'actionName'.
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>none</b><br/>The client application is required to continue to authenticate.</li>
                    <li><b>authenticated</b><br/>The client application is already authenticated through basic access flows.</li>
                    <li><b>degraded</b><br/>The client application is already authenticated through degraded access flows.</li>
                    <li><b>authenticatedSSO</b><br/>The client application is already authenticated through single sign-on access flows.</li>
                    <li><b>pfs_fallback</b><br/>The client application is required to fall back to basic authentication flow due to missing or invalid <a href="../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md">AP-Partner-Framework-Status</a> header value.</li>
                    <li><b>configuration_fallback</b><br/>The client application is required to fall back to basic authentication flow due to partner single sign-on configuration on Adobe Pass backend.</li>
                    <li><b>missing_parameters_fallback</b><br />The client application must revert to the resume flow due to a missing or invalid parameter.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">missingParameters</td>
               <td>
                    The missing parameters that need to be provided in order to complete the basic authentication flow.
                    <br/><br/>
                    This field is present when the partner single sign-on flow cannot proceed.
               </td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">url</td>
               <td>The URL where the client application needs to navigate.</td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">code</td>
               <td>
                    The authentication code that can be used on a secondary application to resume the authentication session.
                    <br/><br/>
                    This field is present when the partner single sign-on flow cannot proceed.
               </td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">authenticationRequest</td>
               <td>
                    The partner authentication request to be used in the authentication flow with the partner outside of Adobe Pass Authentication system.
                    <br/><br/>
                    This field is present when the partner single sign-on flow can proceed.
                    <br/><br/>
                    JSON object having the following attributes:
                    <ul>
                        <li><b>type</b><br/>Indicates the type of protocol supported by the MVPD (SAML only).</li>
                        <li><b>request</b><br/>The SAML request.</li>
                        <li><b>attributesNames</b><br/>The SAML request attributes.</li>
                    </ul>
               </td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">sessionId</td>
               <td>The opaque identifier that can be used for tracking user activity.</td>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">mvpd</td>
               <td>The internal unique identifier associated with the Identity Provider during onboarding process.</td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">serviceProvider</td>
               <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">notBefore</td>
               <td>The timestamp in milliseconds before which the authentication code is not valid.</td>
               <td>optional</td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">notAfter</td>
               <td>The timestamp in milliseconds after which the authentication code is not valid.</td>
               <td>optional</td>
            </tr>
         </table>
      </td>
</table>

### Error {#error}

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
      <td>The response body may provide additional error information that adheres to the <a href="../../../../features-standard/error-reporting/enhanced-error-codes.md">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples}

### 1. Retrieve partner authentication request

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/sessions/sso/Apple HTTP/1.1
 
    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/x-www-form-urlencoded
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAiYWNjZXNzU3RhdHVzIjogImdyYW50ZWQiCiAgICB9LAogICAgImZyYW1ld29ya1Byb3ZpZGVySW5mbyIgOiB7CiAgICAgICJpZCIgOiAiQ2FibGV2aXNpb24iLAogICAgICAiZXhwaXJhdGlvbkRhdGUiIDogIjIwMjU0MzA2MzYwMDAiCiAgICB9Cn0=
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:

domainName=adobe.com&redirectUrl=https%3A%2F%2Fadobe.com
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK  

Content-Type: application/json;charset=UTF-8

{
    "actionName": "partner_profile",
    "actionType": "direct",
    "reasonType": "none",
    "url": "/api/v2/REF30/profiles/sso/Apple",
    "sessionId": "83c046be-ea4b-4581-b5f2-13e56e69dee9",
    "mvpd": "Cablevision",
    "serviceProvider": "REF30",
    "authenticationRequest": {
        "type": "saml",
        "request": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRG....",
        "attributesNames": ["uid", "NameID", "uniqueId"]
   }
}    
```

>[!ENDTABS]

### 2. Retrieve partner authentication request, but degradation is applied

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/sessions/sso/Apple HTTP/1.1
 
    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/x-www-form-urlencoded
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAiYWNjZXNzU3RhdHVzIjogImdyYW50ZWQiCiAgICB9LAogICAgImZyYW1ld29ya1Byb3ZpZGVySW5mbyIgOiB7CiAgICAgICJpZCIgOiAiJHtkZWdyYWRlZE12cGR9IiwKICAgICAgImV4cGlyYXRpb25EYXRlIiA6ICIyMDI1NDMwNjM2MDAwIgogICAgfQp9
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:

domainName=adobe.com&redirectUrl=https%3A%2F%2Fadobe.com
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
    "actionName": "authorize",
    "actionType": "direct",
    "reasonType": "degraded",
    "url": "/api/v2/REF30/decisions/authorize/${degradedMvpd}",
    "sessionId": "14d4f239-e3b1-4a4a-b8b3-6395b968a260",
    "mvpd": "${degradedMvpd}",
    "serviceProvider": "REF30"
}
```

>[!ENDTABS]

### 3. Retrieve partner authentication request, but fall backs to basic authentication flow due to missing or invalid AP-Partner-Framework-Status header value

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/sessions/sso/Apple HTTP/1.1
 
    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/x-www-form-urlencoded
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAiYWNjZXNzU3RhdHVzIjogImRlbmllZCIKICAgIH0sCiAgICAiZnJhbWV3b3JrUHJvdmlkZXJJbmZvIiA6IHt9Cn0=
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:

domainName=adobe.com&redirectUrl=https%3A%2F%2Fadobe.com
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK  

Content-Type: application/json;charset=UTF-8

{
    "actionName": "authenticate",
    "actionType": "interactive",
    "reasonType": "pfs_fallback",
    "url": "/api/v2/authenticate/REF30/OKTWW2W",
    "code": "OKTWW2W",
    "sessionId": "748f0b9e-a2ae-46d5-acd9-4b4e6d71add7",
    "mvpd": "Cablevision",
    "serviceProvider": "REF30",
    "notBefore": "1733735289035",
    "notAfter": "1733737089035"
}
```

>[!ENDTABS]

### 4. Retrieve partner authentication request, but fall backs to basic authentication flow due to partner single sign-on configuration on Adobe Pass backend

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/sessions/sso/Apple HTTP/1.1
 
    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/x-www-form-urlencoded
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAiYWNjZXNzU3RhdHVzIjogImdyYW50ZWQiCiAgICB9LAogICAgImZyYW1ld29ya1Byb3ZpZGVySW5mbyIgOiB7CiAgICAgICJpZCIgOiAiQ2FibGV2aXNpb24iLAogICAgICAiZXhwaXJhdGlvbkRhdGUiIDogIjIwMjU0MzA2MzYwMDAiCiAgICB9Cn0=
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:

domainName=adobe.com&redirectUrl=https%3A%2F%2Fadobe.com
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK  

Content-Type: application/json;charset=UTF-8

{
    "actionName": "authenticate",
    "actionType": "interactive",
    "reasonType": "configuration_fallback",
    "url": "/api/v2/authenticate/REF30/OKTWW2W",
    "code": "OKTWW2W",
    "sessionId": "748f0b9e-a2ae-46d5-acd9-4b4e6d71add7",
    "mvpd": "Cablevision",
    "serviceProvider": "REF30",
    "notBefore": "1733735289035",
    "notAfter": "1733737089035"
}
```

>[!ENDTABS]

### 5. Retrieve partner authentication request, but fall backs to basic authentication flow due to missing parameters

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/sessions/sso/Apple HTTP/1.1
 
    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/x-www-form-urlencoded
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAiYWNjZXNzU3RhdHVzIjogImdyYW50ZWQiCiAgICB9LAogICAgImZyYW1ld29ya1Byb3ZpZGVySW5mbyIgOiB7CiAgICAgICJpZCIgOiAiQ2FibGV2aXNpb24iLAogICAgICAiZXhwaXJhdGlvbkRhdGUiIDogIjIwMjU0MzA2MzYwMDAiCiAgICB9Cn0=
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:
        
domainName=adobe.com
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK  

Content-Type: application/json;charset=UTF-8

{
    "actionName": "resume",
    "actionType": "direct",
    "reasonType": "missing_parameters_fallback",
    "missingParameters": [
          "redirectUrl"
    ],
    "url": "/api/v2/REF30/sessions/SB7ZRIO",
    "code": "SB7ZRIO",
    "sessionId": "1476173f-5088-43b8-b7c3-8cf3a185de0a",
    "mvpd": "Cablevision",
    "serviceProvider": "REF30",
    "notBefore": "1733735289035",
    "notAfter": "1733737089035"
}
```

>[!ENDTABS]
