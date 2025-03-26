---
title: Retrieve profile for specific code
description: REST API V2 - Retrieve profile for specific code
exl-id: d6ead7d5-de5f-4033-8115-980953a370c0
---
# Retrieve profile for specific code {#retrieve-profile-for-specific-code}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

>[!MORELIKETHIS]
>
> Make sure to also visit the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general).

## Request {#request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/api/v2/{serviceProvider}/profiles/code/{code}</td>
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
      <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">code</td>
      <td>The authentication code obtained after creating the authentication session on the streaming device.</td>
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
      <td style="background-color: #DEEBFF;">AP-TempPass-Identity</td>
      <td>The generation of the user unique identifier payload is described in the <a href="../../appendix/headers/rest-api-v2-appendix-headers-ap-temppass-identity.md">AP-TempPass-Identity</a> header documentation.</td>
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
        The response body contains a map of valid profiles, which may be empty.
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
      <td>403</td>
      <td>Forbidden</td>
      <td>
        The temporary access time-to-live (TTL) is expired or maximum number of resources is exceeded, the client needs to indicate the user to initiate a basic authentication flow using a regular MVPD. The response body may contain error information that adheres to the <a href="../../../../features-standard/error-reporting/enhanced-error-codes.md">Enhanced Error Codes</a> documentation.
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
      <td style="background-color: #DEEBFF;">profiles</td>
      <td>
        JSON containing a map of key, value pairs.
        <br/><br/>
        The key element is defined by the following value:
        <table style="table-layout:auto">
            <tr>
               <th style="background-color: #EFF2F7;">Value</th>
               <th style="background-color: #EFF2F7"></th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">mvpd</td>
               <td>The internal unique identifier associated with the Identity Provider during onboarding process.</td>
               <td><i>required</i></td>
            </tr>
         </table>
         The value element is defined by the following attributes:
         <table style="table-layout:auto">
            <tr>
               <th style="background-color: #EFF2F7;">Attribute</th>
               <th style="background-color: #EFF2F7"></th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">notBefore</td>
               <td>The timestamp before which the profile is not valid.</td>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">notAfter</td>
               <td>The timestamp after which the profile is not valid.</td>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">issuer</td>
               <td>
                  The entity that owns the profile.
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>mvpd (e.g., Spectrum, Cablevision, etc.)</b><br/>The profile was created as a result of: basic authentication.</li>
                    <li><b>Adobe</b><br/>The profile was created as a result of: degraded access, temporary access.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">type</td>
               <td>
                  The type of the profile.
                  <br/><br/>
                  The possible values are:
                  <ul>
                    <li><b>regular</b><br/>The profile was created as a result of: basic authentication.</li>
                    <li><b>degraded</b><br/>The profile was created as a result of: degraded access.</li>
                    <li><b>temporary</b><br/>The profile was created as a result of: temporary access.</li>
                  </ul>
               <td><i>required</i></td>
            </tr>
            <tr>
               <td style="background-color: #DEEBFF;">attributes</td>
               <td>
                    JSON containing a map of key, value pairs.
                    <br/><br/>
                    The key element is defined by user metadata attributes and can be:
                    <ul>
                        <li>Mandatory, like 'userID'</li>
                        <li>Non-mandatory, like 'zip', 'householdID', 'maxRating', etc.</li>
                    </ul>
                    The values for the attributes can be:
                    <ul>
                        <li>simple</li>
                        <li>list</li>
                        <li>map</li>
                    </ul>
                    User metadata becomes available after the authentication flow completes, but certain metadata attributes may be updated during the authorization flow, depending on the MVPD and the specific metadata attribute in question.
               </td>
               <td><i>required</i></td>
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
      <td>400, 401, 403, 405, 500</td>
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

### 1. Retrieve profile for specific code obtained through basic authentication

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/v2/REF30/profiles/code/XTC98W HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)
```

>[!TAB Response]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
    "profiles": {
        "Cablevision": {
            "notBefore": 1623943955,
            "notAfter": 1623951155,
            "issuer": "Cablevision",
            "type": "regular",
            "attributes": {
                "userID": {
                    "value": "BASE64_value_userId",
                    "state": "plain"
                },
                "householdID": {
                    "value": "BASE64_value_householdId",
                    "state": "plain"
                },
                "zip": {
                    "value": "BASE64_value_zip",
                    "state": "enc"
                }
            }
        }
     }
}
```

>[!ENDTABS]

### 2. Retrieve profile for specific code while basic TempPass is selected

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/v2/REF30/profiles/code/XTC98W HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)
```

>[!TAB Response - Available]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
    "profiles": {
        "TempPass_TEST40": {
            "notBefore": 1697718650206,
            "notAfter": 1697718710206,
            "issuer": "Adobe",
            "type": "temporary",
            "attributes": {
                "expiration_date": {
                    "value": 1697718710206,
                    "state": "plain"
                },
                "userID": {
                    "value": "temppass_0bdf451aa9c8fa60e80f6b99ab48310c73b480f1",
                    "state": "plain"
                }
            }
        }
    }
}
```

>[!TAB Response - Duration Limit Exceeded]

```HTTPS
HTTP/1.1 403 Forbidden

Content-Type: application/json;charset=UTF-8

{
    "status": 403,
    "code": "temporary_access_duration_limit_exceeded",
    "message": "The temporary access duration limit has been exceeded.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "authentication"
}
```

>[!TAB Response - Invalid Configuration]

```HTTPS
HTTP/1.1 500 Internal Server Error

Content-Type: application/json;charset=UTF-8

{
    "status": 500,
    "code": "invalid_configuration_temporary_access",
    "message": "The temporary access configuration is invalid.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "configuration"
}
```

>[!ENDTABS]

### 3. Retrieve profile for specific code while promotional TempPass is selected

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/v2/REF30/profiles/code/XTC98W HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    AP-TempPass-Identity: eyJlbWFpbCI6ImZvb0BiYXIuY29tIn0=
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)
```

>[!TAB Response - Available]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
    "profiles": {
        "flexibleTempPass": {
            "notBefore": 1697720528524,
            "notAfter": 1697720588524,
            "issuer": "Adobe",
            "type": "temporary",
            "attributes": {
                "remaining_resources": {
                    "value": 1,
                    "state": "plain"
                },
                "used_assets": {
                    "value": [
                        "res04",
                        "res02",
                        "res03",
                        "res01"
                    ],
                    "state": "plain"
                },
                "expiration_date": {
                    "value": 1697720528524,
                    "state": "plain"
                },
                "userID": {
                    "value": "temppass_0bdf451aa9c8fa60e80f6b99ab48310c73b480f1",
                    "state": "plain"
                }
            }
        }
    }
}
```

>[!TAB Response - Duration Limit Exceeded]

```HTTPS
HTTP/1.1 403 Forbidden

Content-Type: application/json;charset=UTF-8

{
    "status": 403,
    "code": "temporary_access_duration_limit_exceeded",
    "message": "The temporary access duration limit has been exceeded.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "authentication"
}
```

>[!TAB Response - Resources Limit Exceeded]

```HTTPS
HTTP/1.1 403 Forbidden

Content-Type: application/json;charset=UTF-8

{
    "status": 403,
    "code": "temporary_access_resources_limit_exceeded",
    "message": "The temporary access resources limit has been exceeded.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "authentication"
}
```

>[!TAB Response - Invalid Configuration]

```HTTPS
HTTP/1.1 500 Internal Server Error

Content-Type: application/json;charset=UTF-8

{
    "status": 500,
    "code": "invalid_configuration_temporary_access",
    "message": "The temporary access configuration is invalid.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "configuration"
}
```

>[!TAB Response - Invalid Identity]

```HTTPS
HTTP/1.1 400 Bad Request

Content-Type: application/json;charset=UTF-8

{
    "status": 400,
    "code": "invalid_header_identity_for_temporary_access",
    "message": "The identity for temporary access header value is missing or invalid.",
    "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
    "action": "none"
}
```

>[!ENDTABS]

### 4. Retrieve profile for specific code while degradation is applied

>[!BEGINTABS]

>[!TAB Request]

```HTTPS
GET /api/v2/REF30/profiles/code/XTC98W HTTP/1.1

    Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJjNGZjM2U3ZS0xMmQ5LTQ5NWQtYjc0Mi02YWVhYzhhNDkwZTciLCJuYmYiOjE3MjQwODc4NjgsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpOmNsaWVudDp2MiIsImV4cCI6MTcyNDEwOTQ2OCwiaWF0IjoxNzI0MDg3ODY4fQ.DJ9GFl_yKAp2Qw-NVcBeRSnxIhqrwxhns5T5jU31N2tiHxCucKLSQ5guBygqkkJx6D0N_93f50meEEyfb7frbHhVHHwmRjHYjkfrWqHCpviwVjVZKKwl8Y3FEMb0bjKIB8p_E3txX9IbzeNGWRufZBRh2sxB5Q9B7XYINpVfh8s_sFvskrbDu5c01neCx5kEagEW5CtE0_EXTgEb5FSr_SfQG3UUu_iwlkOggOh_kOP_5GueElf9jn-bYBMnpObyN5s-FzuHDG5Rtac5rvcWqVW2reEqFTHqLI4rVC7UKQb6DSvPBPV4AgrutAvk30CYgDsOQILVyrjniincp7r9Ww
    Accept: application/json
    User-Agent: Mozilla/5.0 (Apple TV; U; CPU AppleTV5,3 OS 11.0 like Mac OS X; en_US)
```

>[!TAB Response - AuthNAll Degradation]

```HTTPS
HTTP/1.1 200 OK

Content-Type: application/json;charset=UTF-8

{
    "profiles": {
        "${degradedMvpd}": {
            "notBefore": 1697719042666,
            "notAfter": 1697719102666,
            "issuer": "Adobe",
            "type": "degraded",
            "attributes":
                "userID": {
                    "value": "95cf93bcd183214a0bdf451aa9c8fa60e80f6b99ab48310c73b480f1",
                    "state": "plain"
                }
            }
        }
    }
}
```

>[!IMPORTANT]
>
> `95cf93bcd183214a` is a degradation specific prefix.

>[!ENDTABS]
