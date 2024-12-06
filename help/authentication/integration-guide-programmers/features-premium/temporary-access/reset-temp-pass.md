---
title: Reset Temp Pass
description: Reset Temp Pass
exl-id: ab39e444-eab2-4338-8d09-352a1d5135b6
---

# Reset Temp Pass {#reset-temp-pass}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Before using the Reset Temp Pass API, ensure the following prerequisites are met: 
>
> * Obtain the client credentials as described in the [Retrieve client credentials](../../rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md) API documentation.
> * Obtain the access token as described in the [Retrieve access token](../../rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) API documentation.
>
> Refer to the [Dynamic Client Registration Overview](../../rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation for more information about how to create a registered application and download the software statement.

In order to **reset a specific Temp Pass for a device or all devices**, Adobe Pass Authentication provides Programmers with a *public* web API:

```url

DELETE https://mgmt.auth.adobe.com/reset-tempass/v3/reset

```

*   **Protocol:** HTTPS
*   **Host:**
    * Release - mgmt.auth.adobe.com
    * Prequal - mgmt-prequal.auth.adobe.com
*   **Path:** /reset-tempass/v3/reset 
*   **Query parameters:** device_id(when no value is provided, defaults to all), requestor_id (required), mvpd_id (required), appId, deviceUser, environment
*   **Headers:** Authorization: Bearer <access_token_here>
*   **Response:** 
    *   Success - HTTP 204
    *   Failure:xw
        * HTTP 400 for an incorrect request
        * HTTP 401 if the access is denied. The client MUST request a new access_token.
        * HTTP 403 if the client id is no longer permitted to perform requests. New client credentials should be generated.


For example:

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"

```

In order to **reset Flexible Temp Pass for a generic key or all keys**, Adobe Pass Authentication provides Programmers with a *public* web API:

```url

DELETE https://mgmt.auth.adobe.com/reset-tempass/v3/reset/generic

```

*   **Protocol:** HTTPS
*   **Host:**
    * Release - mgmt.auth.adobe.com
    * Prequal - mgmt-prequal.auth.adobe.com
*   **Path:** /reset-tempass/v3/reset/generic
*   **Query parameters:** key(when no value is provided, defaults to all), requestor_id (required), mvpd_id (required), environment
*   **Headers:** Authorization: Bearer <access_token_here>
*   **Response:**
    *   Success - HTTP 204
    *   Failure:
        * HTTP 400 for an incorrect request
        * HTTP 401 if the access is denied. The client MUST request a new access_token.
        * HTTP 403 if the client id is no longer permitted to perform requests. New client credentials should be generated.


For example, setting the *Generic Key* to an E-mail address hash (for
Temp Pass MVPDs that support this kind of functionality) will yield the
following HTTP call (the E-mail is `user@domain.com` its SHA-256
hash is `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer <access_token_here>"
"https://mgmt.auth.adobe.com/reset-tempass/v3/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```
