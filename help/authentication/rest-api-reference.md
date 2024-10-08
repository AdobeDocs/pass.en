---
title: REST API Reference
description: Rest api reference
exl-id: 67e4639e-db0b-4400-bb81-e214263e8395
---
# REST API Reference {#rest-api-reference}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Throttling mechanism

The Adobe Pass Authentication REST API is governed by a [Throttling mechanism](/help/authentication/throttling-mechanism.md).

## Response Formats {#response-formats}


>[!NOTE] 
>
> The APIs provided in these services can return responses in either XML or JSON (for APIs that return a response). There are 3 different ways to specify the response format in the request:
>
>* Set HTTP Accept Header to `application/xml` or `application/json`.
>* In the request payload, specify the parameter `format=xml` or `format=json`.
>* Call the web service endpoint with extension `.xml` or `.json`. For example, `/regcode.xml` or `/regcode.json`
>
>You can specify any ONE of the above methods. Specifying multiple methods with conflicting formats may result in errors or undesirable output.

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Web Services Summary {#web_srvs_summary}

The table below lists the available web services for the clientless approach. Click the web services endpoints for more information (sample request and response, input parameters, HTTP methods, etc.)

  
| Sr  | Web Service Endpoint | Description | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | Hosted At | Called By |
| --- | --- | --- | --- | --- | --- |
| 1.  | [<REGGIE_FQDN>/reggie/v1/  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | Returns randomly generated registration Code and login Page URI | 2   | Adobe  </br>Reg Code Service | Smart Device |
| 2.  | [<REGGIE_FQDN>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | Returns registration code record containing registration code UUID, registration code, and hashed device ID | 8   | Adobe  </br>Reg Code Service | Adobe Pass Authentication |
| 3.  | [<SP_FQDN>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | Returns list of configured MVPDs for the requestor | 5   | Adobe  </br>Adobe Pass  </br>authentication  </br>Service | Login  </br>Web  </br>App |
| 4.  | [<SP_FQDN>/api/v1/authenticate](/help/authentication/initiate-authentication.md) | Initiates the AuthN process by informing MVPD selection event. Creates a record on authentication database, which is reconciled when a successful response is received from MVPD (Step 13) | 7   | Adobe  </br>Adobe Pass  </br>authentication  </br>Service | Login  </br>Web  </br>App |
| 5.  | SAML Assertion Consumer | Existing SAML workflow between Adobe Pass Authentication and MVPD | 13  | Adobe Pass  </br>authentication  </br>Service | Adobe Pass Authentication |
| 6.  | [<SP_FQDN>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | The Login Web App can check if the attempted login flow was successful |     | Adobe Pass  </br>authentication   </br>Service | Login   </br>Web   </br>App |
| 7.  | [<SP_FQDN>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Gets AuthN token related metadata | 15  | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 8.  | [<REGGIE_FQDN>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | Deletes the reg code record and releases the reg code for reuse | 16  | Adobe  </br>Reg Code Service | Adobe Pass Authentication |
| 9.  | [<SP_FQDN>/api/v1/authorize](/help/authentication/initiate-authorization.md) | Obtains authorization response. | 17  | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 10. | [<SP_FQDN>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | Indicates whether the device has an unexpired AuthN token. |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 11. | [<SP_FQDN>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Returns the AuthN token if found. |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 12. | [<SP_FQDN>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | Returns the AuthZ token if found. |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 13. | [<SP_FQDN>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | Returns the Short Media Token if found - same as /api/v1/mediatoken |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 14. | [<SP_FQDN>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | Obtains Short Media Token |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 15. | [<SP_FQDN>/api/v1/preauthorize](/help/authentication/retrieve-list-of-preauthorized-resources.md) | Retrieves the list of preauthorized resource |     | Adobe Pass  </br>authentication  </br>Service | Smart Device |
| 16. | [<SP_FQDN>/api/v1/preauthorize/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | Retrieves the list of preauthorized resources |     | Adobe Pass  </br>authentication  </br>Service | Login Web App |
| 17. | [<SP_FQDN>/api/v1/logout](/help/authentication/initiate-logout.md) | Remove AuthN and AuthZ tokens from storage |     | Adobe Pass  </br>authentication   </br>Service | Smart Device |
| 18. | [<SP_FQDN>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | Gets user metadata after authentication flow completes | N/A | N/A | Smart Device |
| 19. | [<SP_FQDN>/api/v1/authenticate/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | Create an authentication token for Temp Pass or Promotional Temp Pass | N/A | Adobe Pass  </br>authentication  </br>Service | Smart Device |


## REST API Security {#security}

All Adobe Pass Authentication REST APIs must be called using the HTTPS protocol for secure communication. In addition, most of the APIs called should contain an access token obtained as described in the [Retrieve access token](./dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md) API documentation.
