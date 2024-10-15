---
title: Retrieve preauthorization decisions using specific mvpd
description: REST API V2 - Retrieve preauthorization decisions using specific mvpd
exl-id: 8647e4fb-00b6-45cd-b81b-d00618b2e08b
---
# Retrieve preauthorization decisions using specific mvpd {#retrieve-preauthorization-decisions-using-specific-mvpd}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

## Request {#request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}</td>
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
      <td style="background-color: #DEEBFF;">mvpd</td>
      <td>The internal unique identifier associated with the Identity Provider during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Body Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">resources</td>
      <td>The list of resources that require an MVPD decision before they could be displayed.</td>
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
         It must be application/json.
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
      <td style="background-color: #DEEBFF;">Adobe-Subject-Token</td>
      <td>
        The generation of the single sign-on payload for the Platform Identity method is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-adobe-subject-token.md">Adobe-Subject-Token</a> header documentation.
        <br/><br/>
        For more details about single sign-on enabled flows using a platform identity, refer to the <a href="../../flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md">Single sign-on using platform identity flows</a> documentation.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">AD-Service-Token</td>
      <td>
        The generation of the single sign-on payload for the Service Token method is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-ad-service-token.md">AD-Service-Token</a> header documentation.
        <br/><br/>
        For more details about single sign-on enabled flows using a service token, refer to the <a href="../../flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md">Single sign-on using service token flows</a> documentation.
      </td>
      <td>optional</td>
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
      <td style="background-color: #DEEBFF;">Accept</td>
      <td>
         The media type accepted by the client application.
         <br/><br/>
         If specified, it must be application/json.
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
        The response body contains a list of decisions with additional information.
      </td>
   </tr>
      <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again. The response body may contain error information that adheres to the <a href="../../../enhanced-error-codes.md">Enhanced Error Codes</a> documentation.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="../../../dcr-api/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
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
        The server side encountered an issue. The response body may contain error information that adheres to the <a href="../../../enhanced-error-codes.md">Enhanced Error Codes</a> documentation.
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
      <td style="background-color: #DEEBFF;">decisions</td>
      <td>
         JSON containing a list of elements, each element having the following attributes:
         <table style="table-layout:auto">
            <tr>
               <th style="background-color: #EFF2F7;">Attribute</th>
               <th style="background-color: #EFF2F7"></th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
                <td style="background-color: #DEEBFF;">resource</td>
                <td>The resource identifier for which the preauthorization decision is returned.</td>
                <td><i>required</i></td>
            </tr>
            <tr>
                <td style="background-color: #DEEBFF;">serviceProvider</td>
                <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
                <td><i>required</i></td>
            </tr>
            <tr>
                <td style="background-color: #DEEBFF;">mvpd</td>
                <td>The internal unique identifier associated with the Identity Provider during onboarding process.</td>
                <td><i>required</i></td>
            </tr>
            <tr>
                <td style="background-color: #DEEBFF;">authorized</td>
                <td>The decision status for the resource, which can be either 'true' or 'false'.</td>
                <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">source</td>
               <td>
                  Information about decision source:
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>mvpd</b><br/>Decision is issued by the MVPD preauthorization endpoint.</li>
                    <li><b>degradation</b><br/>Decision is issued as a result of degraded access.</li>
                    <li><b>temppass</b><br/>Decision is issued as a result of temporary access.</li>
                    <li><b>dummy</b><br/>Decision is issued as a result of dummy preauthorization feature.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">error</td>
               <td>The error provides additional information about the 'Deny' decision that adheres to the <a href="../../../enhanced-error-codes.md">Enhanced Error Codes</a> documentation.</td>
               <td>optional</td>
            </tr>
         </table>
      </td>
      <td><i>required</i></td>
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
      <td>The response body may provide additional error information that adheres to the <a href="../../../enhanced-error-codes.md">Enhanced Error Codes</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

## Samples {#samples}

### 1. Retrieve preauthorization decisions using specific mvpd

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/decisions/preauthorize/Cablevision HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/json
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:       

{
    "resources": ["resource1", "resource2", "resource3"]
}
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
   "decisions": [
      {
         "resource": "resource1 ",
         "serviceProvider": "REF30",
         "mvpd": "Cablevision",
         "source": "mvpd",
         "authorized": true
      },
      {
         "resource": "resource2",
         "serviceProvider": "REF30",
         "mvpd": "Cablevision",
         "source": "mvpd",
         "authorized": true
      },
      {
         "resource": "resource3",
         "serviceProvider": "REF30",
         "mvpd": "Cablevision",
         "source": "mvpd",
         "authorized": false,
         "error": {
            "status": 403,
            "code": "preauthorization_denied_by_mvpd",
            "message": "The MVPD has returned a \"Deny\" decision when requesting pre-authorization for the specified resource.",
            "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
            "action": "none"
         }
      }
   ]
}
```

>[!ENDTABS]

### 2. Retrieve preauthorization decisions using specific mvpd while degradation is applied

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
POST /api/v2/REF30/decisions/preauthorize/${degradedMvpd} HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Content-Type: application/json
    AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
    X-Device-Info: ewoJInByaW1hcnlIYXJkd2FyZVR5cGUiOiAiU2V0VG9wQm94IiwKCSJtb2RlbCI6ICJUViA1dGggR2VuIiwKCSJtYW51ZmFjdHVyZXIiOiAiQXBwbGUiLAoJIm9zTmFtZSI6ICJ0dk9TIgoJIm9zVmVuZG9yIjogIkFwcGxlIiwKCSJvc1ZlcnNpb24iOiAiMTEuMCIKfQ==
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)

Body:

{
    "resources": ["REF30", "apasstest1"]
}
```

>[!TAB Response - AuthNAll Degradation]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8
 
{
    "decisions": [
        {
            "resource": "REF30",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": true
        }
        {
            "resource": "apasstest1",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": true
        }
    ]
}
```

>[!TAB Response - AuthZAll Degradation]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8
 
{
    "decisions": [
        {
            "resource": "REF30",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": true
        }
        {
            "resource": "apasstest1",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": true
        }
    ]
}
```

>[!TAB Response - AuthZNone Degradation]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8
 
{
    "decisions": [
        {
            "resource": "REF30",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": false,
            "error": {
                "status": 403,
                "code": "authorization_denied_by_degradation_rule",
                "message": "The integration has an AuthZNone rule applied for the requested resources",
                "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
                "action": "none"
            }
        }
        {
            "resource": "apasstest1",
            "serviceProvider": "REF30",
            "mvpd": "${degradedMvpd}",
            "source": "degradation",
            "authorized": false,
            "error": {
                "status": 403,
                "code": "authorization_denied_by_degradation_rule",
                "message": "The integration has an AuthZNone rule applied for the requested resources",
                "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
                "action": "none"
            }
        }
    ]
}
```

>[!ENDTABS]
