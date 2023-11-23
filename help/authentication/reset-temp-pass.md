---
title: Reset Temp Pass
description: Reset Temp Pass
---
# Reset Temp Pass {#reset-temp-pass}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.
>
>In order to use the Reset Temp Pass API, you will need to: 
>- ask the support team for a software  statement for your registered application
>- obtain an access token based on [Dynamic Client Registration](dynamic-client-registration.md)
> 
 
In order to **reset a specific Temp Pass**, Adobe Pass Authentication provides Programmers with a *public* web API:

- **Environment:** specifies the Adobe Pay-TV pass server endpoint that will receive the reset Temp Pass network call. Possible values: **Prequal** (*mgmt-prequal.auth.adobe.com*), **Release** (*mgmt.auth.adobe.com*) or **Custom** (reserved for Adobe internal testing).
- **OAuth2 Access Token:** the OAuth2 token is necessary for authorizing the Programmer for Adobe Pay-TV authentication. Such a token can be obtained from [Dynamic Client Registration](dynamic-client-registration.md).
- **Temp Pass ID:** the unique ID for the Temp Pass MVPD to be reset.(a programmer can use multiple Temp Pass MVPDs and want to reset a specific one)
- **Generic Key:** some Temp Pass MVPDs (i.e. [Promotional temp pass](promotional-temp-pass.md)).

All the above parameters (except the *Generic Key*) are mandatory. Here is an example of parameters and the associated network call(the example is in the form of a *curl *command):

- **Environment:** Release (*mgmt.auth.adobe.com*)
- **OAuth2 Access Token:** <access_token> from [Dynamic Client Registration](dynamic-client-registration.md)
- **Programmer ID:** REF
- **Temp Pass ID:** TempPassREF
- **Generic Key:** null (no value provided)

```curl
curl -X DELETE -H "Authorization:Bearer <access_token_here>" "https://mgmt.auth.adobe.com/reset-tempass/v3/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

a DELETE HTTP request will be made to the **/reset** endpoint, passing the *OAuth2 Access Token* in the Authorization header and the *Device ID*, *Requestor ID* and *Temp Pass ID (MVPD ID)* as parameters.

If the Programmer supplies a value for the *Generic Key*, another HTTP call will be performed (this time to the **/reset/generic** endpoint), passing the *Generic Key* inside the *key* request parameter.

For example, setting the *Generic Key* to an E-mail address hash (for
Temp Pass MVPDs that support this kind of functionality) will yield the
following HTTP call (the E-mail is `user@domain.com` its SHA-256
hash is `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer <access_token_here>"
"https://mgmt.auth.adobe.com/reset-tempass/v3/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

 
In order to **reset a specific Temp Pass for all devices**, Adobe Pass Authentication provides Programmers with a *public* web API:

```url

DELETE https://mgmt.auth.adobe.com/reset-tempass/v3/reset

```

>[!NOTE]
>The URL above supersedes the previous reset API. The old reset API (v1) is no longer supported.

-   **Protocol:** HTTPS
-   **Host:**
    - Release - mgmt.auth.adobe.com
    - Prequal - mgmt-prequal.auth.adobe.com
-   **Path:** /reset-tempass/v3/reset 
-   **Query parameters:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
-   **Headers:** Authorization: Bearer <access_token_here>
-   **Response:** 
    -   Success - HTTP 204
    -   Failure:
        - HTTP 400 for an incorrect request
        - HTTP 401 if the access is denied. The client MUST request a new access_token.
        - HTTP 403 if the client id is not longer permitted to perform requests. New client credentials should be generated.


For example:

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"

```
