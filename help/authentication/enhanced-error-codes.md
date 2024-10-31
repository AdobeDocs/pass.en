---
title: Enhanced Error Codes
description: Enhanced Error Codes
exl-id: 2b0a9095-206b-4dc7-ab9e-e34abf4d359c
---
# Enhanced Error Codes {#enhanced-error-codes}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Enhanced Error Codes represent an Adobe Pass Authentication feature that provides additional error information to client applications integrated with:

* Adobe Pass Authentication REST APIs:
  * [REST API v1](./rest-api-overview.md)
  * [REST API v2](./rest-api-v2/apis/rest-api-v2-apis-overview.md)
* Adobe Pass Authentication SDKs Preauthorize API:
  * [JavaScript SDK (Preauthorize API)](./preauthorize-api-javascript-sdk.md)
  * [iOS/tvOS SDK (Preauthorize API)](./preauthorize-api-ios-tvos-sdk.md)
  * [Android SDK (Preauthorize API)](./preauthorize-api-android-sdk.md)

  _(*) Preauthorize API is the only Adobe Pass Authentication SDK API that provides support for Enhanced Error Codes._

>[!IMPORTANT]
>
> Applications that integrate Adobe Pass Authentication REST API v2 will benefit from Enhanced Error Codes by default without requiring additional configuration.
>
> <br/>
>
> Applications that integrate Adobe Pass Authentication REST API v1 or SDKs Preauthorize API can benefit from Enhanced Error Codes only if the feature is explicitly enabled.
>
> <br/>
>
> To explicitly enable this feature, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) for assistance.

## Representation {#enhanced-error-codes-representation}

Enhanced Error Codes can be represented in `JSON` or `XML` format depending on the integrated Adobe Pass Authentication API and the used "Accept" header value (i.e., `application/json` or `application/xml`):

| Adobe Pass Authentication API | JSON    | XML     |
|-------------------------------|---------|---------|
| REST API v1                   | &check; | &check; |
| REST API v2                   | &check; |         |
| SDKs Preauthorize API         | &check; |         |

>[!IMPORTANT]
>
> Adobe Pass Authentication can communicate Enhanced Error Codes to client applications in two forms:
>
> <br/>
>
> * **Top-level error information**: In this case, the ***"error"*** object is located at the top level, therefore the response body can contain only the ***"error"*** object.
> * **Item-level error information**: In this case, the ***"error"*** object is located at the item level, therefore the response body can contain an ***"error"*** object for all items that experienced an error while being serviced.
>
> <br/>
>
> Check the public documentation for each integrated Adobe Pass Authentication API to determine the Enhanced Error Codes representation specifics.

Refer to the following HTTP responses containing Enhanced Error Codes examples represented as `JSON` or `XML`.

>[!BEGINTABS]

>[!TAB REST API v1 - Top-level error information (JSON)]

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json
        
{
  "action": "none",
  "status": 400,
  "code": "invalid_requestor",
  "message": "The requestor parameter is missing or invalid.",
  "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
  "trace": "8bcb17f9-b172-47d2-86d9-3eb146eba85e"
}
```

>[!TAB REST API v1 - Top-level error information (XML)]

```XML
HTTP/1.1 400 Bad Request
Content-Type: application/xml

<error>
  <action>none</action>
  <status>400</status>
  <code>invalid_requestor</code>
  <message>The requestor parameter is missing or invalid.</message>
  <helpUrl>https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html</helpUrl>
  <trace>8bcb17f9-b172-47d2-86d9-3eb146eba85e</trace>
</error>
```

>[!TAB REST API v1 - Item-level error information (JSON)]

```JSON
HTTP/1.1 200 OK
Content-Type: application/json

{
  "resources": [
    {
      "id": "TestStream1",
      "authorized": true
    },
    {
      "id": "TestStream2",
      "authorized": false,
      "error": {
        "action": "retry",
        "status": 403,
        "code": "network_connection_failure",
        "message": "Unable to contact your TV provider services",
        "details": "Your subscription package does not include the \"Live\" channel",
        "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
        "trace": "12f6fef9-d2e0-422b-a9d7-60d799abe353"
      }
    }
  ]
}
```

>[!TAB REST API v2 - Top-level error information (JSON)]

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "action": "none",
  "status": 400,
  "code": "invalid_parameter_service_provider",
  "message": "The service provider parameter value is missing or invalid.",
  "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
  "trace": "12f6fef9-d2e0-422b-a9d7-60d799abe353"
}
```

>[!TAB REST API v2 - Item-level error information (JSON)]

```JSON
HTTP/1.1 200 OK
Content-Type: application/json

{
  "decisions": [
    {
      "resource": "REF30",
      "serviceProvider": "REF30",
      "mvpd": "Cablevision",
      "source": "mvpd",
      "authorized": true,
      "token": {
        "issuedAt": 1697094207324,
        "notBefore": 1697094207324,
        "notAfter": 1697094802367,
        "serializedToken": "PHNpZ25hdHVyZUluZm8..."
      }
    },
    {
      "resource": "REF40",
      "serviceProvider": "REF40",
      "mvpd": "Cablevision",
      "source": "mvpd",
      "authorized": false,
      "error" : {
        "action": "retry",
        "status": 403,
        "code": "network_connection_failure",
        "message": "Unable to contact your TV provider services",
        "details": "Your subscription package does not include the \"Live\" channel",
        "helpUrl": "https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html",
        "trace": "12f6fef9-d2e0-422b-a9d7-60d799abe353"
      }
    }
  ]
}
```

>[!ENDTABS]

Enhanced Error Codes include the following `JSON` fields or `XML` attributes:

| Name      | Type      | Example                                                                                                             | Restricted | Description                                                                                                                                                                                                                                                                                         |
|-----------|-----------|---------------------------------------------------------------------------------------------------------------------|:----------:|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *action*  | *string*  | *retry*                                                                                                             |  &check;   | The Adobe Pass Authentication recommended action that might remediate the situation as defined in this document. <br/><br/> For more details, refer to the [Action](#enhanced-error-codes-action) section.                                                                                          |
| *status*  | *integer* | *403*                                                                                                               |  &check;   | The HTTP response status code as defined in [RFC 7231](https://tools.ietf.org/html/rfc7231#section-6) document. <br/><br/> For more details, refer to the [Status](#enhanced-error-codes-status) section.                                                                                           |
| *code*    | *string*  | *network_connection_failure*                                                                                        |  &check;   | The Adobe Pass Authentication unique identifier code associated with the error as defined in this document. <br/><br/> For more details, refer to the [Code](#enhanced-error-codes-code) section.                                                                                                   |
| *message* | *string*  | *Unable to contact your TV provider services*                                                                       |            | The human readable message that could be displayed to the end user in some cases. <br/><br/> For more details, refer to the [Response Handling](#enhanced-error-codes-response-handling) section.                                                                                                   |
| *details* | *string*  | *Your subscription package does not include the "Live" channel*                                                     |            | The detailed message that could be provided by a services partner in some cases, <br/><br/> This field might not be present in case the services partner does not provide any custom message.                                                                                                       |
| *helpUrl* | *url*     | *https://experienceleague.adobe.com/docs/pass/authentication/auth-features/error-reportn/enhanced-error-codes.html* |            | The Adobe Pass Authentication public documentation URL that links to more information about why this error occurred and possible solutions. <br/><br/> This field holds an absolute URL and should not be inferred from error code, depending on the error context a different URL can be provided. |
| *trace*   | *string*  | *12f6fef9-d2e0-422b-a9d7-60d799abe353*                                                                              |            | The unique identifier for the response that can be used when contacting Adobe Pass Authentication support to troubleshoot specific issues.                                                                                                                                                          |

>[!IMPORTANT]
>
> The **Restricted** column indicates if the respective field holds a value from a finite set, while unrestricted fields can contain any data.
>
> <br/>
>
> Future updates to this document could add values to the finite sets, but will not remove or change existing ones.

### Action {#enhanced-error-codes-representation-action}

Enhanced Error Codes include an "action" field that provides a recommended action that might remediate the situation.

The possible values for the "action" field include:

| Action                   | Description                                                                                                                     | Category                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| none                     | There is no predefined action to remediate this issue, but in some cases this might indicate an improper invocation of the API. | Fix the request context.                   |
| configuration            | The client application requires a configuration change, most of the time conducted through Adobe Pass TVE Dashboard.            | Fix the integration configuration context. | 
| application-registration | The client application requires to register itself again.                                                                       | Fix the client application context.        |
| authentication           | The client application requires to authenticate or re-authenticate the user.                                                    | Fix the client application context.        |
| authorization            | The client application requires to obtain authorization for the specified resource.                                             | Fix the client application context.        |
| retry                    | The client application requires to retry the request.                                                                           | Fix the request context.                   |

_(*) For some errors, multiple actions could be possible solutions, but the "action" field indicates the one with the highest probability of fixing the error._

### Status {#enhanced-error-codes-representation-status}

Enhanced Error Codes include a "status" field that indicates the HTTP status code associated with the error.

The possible values for the "status" field include:

| Code | Reason-Phrase         |
|------|-----------------------|
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 405  | Method Not Allowed    |
| 410  | Gone                  |
| 412  | Precondition Failed   |
| 500  | Internal Server Error |

Enhanced Error Codes with a 4xx "status" usually appear when the error is generated by the client and most of the time it implies that the client requires additional work to fix it.

Enhanced Error Codes with a 5xx "status" usually appear when the error is generated by the server and most of the time it implies that the server requires additional work to fix it.

>[!IMPORTANT]
>
> There are cases when the HTTP response status code is different from the Enhanced Error Code "status" field, especially when interacting with an Adobe Pass Authentication API that communicates Enhanced Error Codes as item-level error information.

### Code {#enhanced-error-codes-representation-code}

Enhanced Error Codes include a "code" field that provides an Adobe Pass Authentication unique identifier associated with the error.

The possible values for the "code" field are aggregated [below](#enhanced-error-codes-list) in two lists based on the integrated Adobe Pass Authentication API.

## Lists {#enhanced-error-codes-lists}

### REST API v1 {#enhanced-error-codes-lists-rest-api-v1}

The table below lists possible Enhanced Error Codes a client application might encounter when integrated with Adobe Pass Authentication REST API v1.

| Action             | Code                                              | Status            | Message                                                                                                                                                                                                                                                                                                                                      |
|--------------------|---------------------------------------------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **none**           | *invalid_requestor*                               | 400               | The requestor parameter is missing or invalid.                                                                                                                                                                                                                                                                                               |
|                    | *invalid_device_info*                             | 400               | The device information is missing or invalid.                                                                                                                                                                                                                                                                                                |
|                    | *invalid_device_id*                               | 400               | The device identifier is missing or invalid.                                                                                                                                                                                                                                                                                                 |
|                    | *missing_resource*                                | 400, 412          | The resource parameter is missing.                                                                                                                                                                                                                                                                                                           |
|                    | *malformed_authz_request*                         | 400, 412          | Authorization request is null or invalid.                                                                                                                                                                                                                                                                                                    |
|                    | *preauthorization_denied_by_mvpd*                 | 403               | The MVPD has returned a “Deny” decision when requesting pre-authorization for the specified resource.                                                                                                                                                                                                                                        |
|                    | *authorization_denied_by_mvpd*                    | 403               | The MVPD has returned a "Deny" decision when requesting authorization for the specified resource.                                                                                                                                                                                                                                            |
|                    | *authorization_denied_by_parental_controls*       | 403               | The MVPD has returned a "Deny" decision due parental controls settings for the specified resource.                                                                                                                                                                                                                                           |
|                    | *internal_error*                                  | 400, 405, 500     | The request failed due to an internal server error.                                                                                                                                                                                                                                                                                          |
| **configuration**  | *unknown_integration*                             | 400, 412          | The integration between the specified programmer and identity provider does not exist. Use the TVE Dashboard to create the required integration.                                                                                                                                                                                             |
|                    | *too_many_resources*                              | 403               | The authorization or preauthorization request failed because too many resources were queried. Please contact support team to properly configure the authorization and preauthorization limitations.                                                                                                                                          |
| **authentication** | *authentication_session_issuer_mismatch*          | 400               | The authorization request failed due to the fact that the indicated MVPD for the authorization flow is different from the one who issued the authentication session. The user must re-authenticate with the desired MVPD in order to continue.                                                                                               |
|                    | *authorization_denied_by_hba_policies*            | 403               | The MVPD has returned a "Deny" decision due home-based authentication policies. The current authentication was obtained using a home-based authentication flow (HBA) but the device is no longer at-home when requesting authorization for the specified resource. The user must re-authenticate with a supported MVPD in order to continue. |
|                    | *authorization_denied_by_session_invalidated*     | 403               | The authentication session was invalidated by the identity provider. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                               |
|                    | *identity_not_recognized_by_mvpd*                 | 403               | The authorization request failed due to the fact that user identity was not recognized by the MVPD.                                                                                                                                                                                                                                          |
|                    | *authentication_session_invalidated*              | 403               | The authentication session was invalidated by the identity provider. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                               |
|                    | *authentication_session_missing*                  | 403, 412          | The authentication session associated with this request could not be retrieved. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                    |
|                    | *authentication_session_expired*                  | 403, 412          | The current authentication session has expired. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                                                    |
|                    | *preauthorization_authentication_session_missing* | 412               | The authentication session associated with this request could not be retrieved. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                    |
|                    | *preauthorization_authentication_session_expired* | 412               | The current authentication session has expired. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                                                    |
| **authorization**  | *authorization_not_found*                         | 403, 404          | No authorization was found for the specified resource. The user must obtain a new authorization in order to continue.                                                                                                                                                                                                                        |
|                    | *authorization_expired*                           | 410               | The previous authorization for the specified resource has expired. The user must obtain a new authorization in order to continue.                                                                                                                                                                                                            | 
| **retry**          | *network_received_error*                          | 403               | There was a read error while retrieving the response from the associated partner service. Retrying the request might solve the issue.                                                                                                                                                                                                        |
|                    | *network_connection_timeout*                      | 403               | There was a connection timeout with the associated partner service. Retrying the request might solve the issue.                                                                                                                                                                                                                              |
|                    | *maximum_execution_time_exceeded*                 | 403               | The request did not complete in the maximum allowed time. Retrying the request might solve the issue.                                                                                                                                                                                                                                        |

### SDKs Preauthorize API {#enhanced-error-codes-lists-sdks-preauthorize-api}

Refer to the previous [section](#enhanced-error-codes-list-rest-api-v1) for possible Enhanced Error Codes a client application might encounter when integrated with Adobe Pass Authentication SDKs Preauthorize API.

### REST API v2 {#enhanced-error-codes-lists-rest-api-v2}

The table below lists possible Enhanced Error Codes a client application might encounter when integrated with Adobe Pass Authentication REST API v2.

| Action                       | Code                                                   | Status | Message                                                                                                                                                                                                                                                                                                                                    |
|------------------------------|--------------------------------------------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **none**                     | *invalid_parameter_service_provider*                   | 400    | The service provider parameter value is missing or invalid.                                                                                                                                                                                                                                                                                |
|                              | *invalid_parameter_mvpd*                               | 400    | The mvpd parameter value is missing or invalid.                                                                                                                                                                                                                                                                                            |
|                              | *invalid_parameter_code*                               | 400    | The code parameter value is missing or invalid.                                                                                                                                                                                                                                                                                            |
|                              | *invalid_parameter_resources*                          | 400    | The resources parameter value is missing or invalid.                                                                                                                                                                                                                                                                                       |
|                              | *invalid_parameter_redirect_url*                       | 400    | The redirect URL parameter value is missing or invalid.                                                                                                                                                                                                                                                                                    |
|                              | *invalid_parameter_partner*                            | 400    | The partner parameter value is missing or invalid.                                                                                                                                                                                                                                                                                         |
|                              | *invalid_parameter_saml_response*                      | 400    | The SAML response parameter value is missing or invalid.                                                                                                                                                                                                                                                                                   |
|                              | *invalid_header_device_info*                           | 400    | The device information header value is missing or invalid.                                                                                                                                                                                                                                                                                 |
|                              | *invalid_header_device_identifier*                     | 400    | The device identifier header value is missing or invalid.                                                                                                                                                                                                                                                                                  |
|                              | *invalid_header_identity_for_temporary_access*         | 400    | The identity for temporary access header value is missing or invalid.                                                                                                                                                                                                                                                                      |
|                              | *invalid_header_pfs_permission_access_not_present*     | 400    | The permission access status value from the partner framework status header is not present.                                                                                                                                                                                                                                                |
|                              | *invalid_header_pfs_permission_access_not_determined*  | 400    | The permission access status value from the partner framework status header is undetermined.                                                                                                                                                                                                                                               |
|                              | *invalid_header_pfs_permission_access_not_granted*     | 400    | The permission access status value from the partner framework status header is not granted.                                                                                                                                                                                                                                                |
|                              | *invalid_header_pfs_provider_id_not_determined*        | 400    | The provider id value from the partner framework status header is not associated with a known mvpd.                                                                                                                                                                                                                                        |
|                              | *invalid_header_pfs_provider_id_mismatch*              | 400    | The provider id value from the partner framework status header does not match the mvpd sent as parameter.                                                                                                                                                                                                                                  |
|                              | *invalid_integration*                                  | 400    | The integration between the specified service provider and mvpd does not exist or is disabled.                                                                                                                                                                                                                                             |
|                              | *invalid_authentication_session*                       | 400    | The authentication session associated with this request is missing or invalid.                                                                                                                                                                                                                                                             |
|                              | *preauthorization_denied_by_mvpd*                      | 403    | The MVPD has returned a “Deny” decision when requesting pre-authorization for the specified resource.                                                                                                                                                                                                                                      |
|                              | *authorization_denied_by_mvpd*                         | 403    | The MVPD has returned a "Deny" decision when requesting authorization for the specified resource.                                                                                                                                                                                                                                          |
|                              | *authorization_denied_by_parental_controls*            | 403    | The MVPD has returned a "Deny" decision due parental controls settings for the specified resource.                                                                                                                                                                                                                                         |
|                              | *authorization_denied_by_degradation_rule*             | 403    | The integration between the specified service provider and mvpd has a degradation rule applied that denies authorization for the requested resources.                                                                                                                                                                                      |
|                              | *internal_server_error*                                | 500    | The request failed due to an internal server error.                                                                                                                                                                                                                                                                                        |
| **configuration**            | *too_many_resources*                                   | 403    | The authorization or preauthorization request failed because too many resources were queried. Please contact support team to properly configure the authorization and preauthorization limitations.                                                                                                                                        |
|                              | *invalid_configuration_user_metadata_certificate*      | 500    | The user metadata certificate configuration is missing or invalid.                                                                                                                                                                                                                                                                         |
|                              | *invalid_configuration_temporary_access*               | 500    | The temporary access configuration is invalid.                                                                                                                                                                                                                                                                                             |
|                              | *invalid_configuration_platform*                       | 500    | The platform configuration is missing or invalid for integration.                                                                                                                                                                                                                                                                          |
|                              | *invalid_configuration_platform_id*                    | 500    | The platform id configuration is missing or invalid.                                                                                                                                                                                                                                                                                       |
|                              | *invalid_configuration_platform_trait*                 | 500    | The platform trait configuration is missing or invalid.                                                                                                                                                                                                                                                                                    |
|                              | *invalid_configuration_platform_category_trait*        | 500    | The platform category trait configuration is missing or invalid.                                                                                                                                                                                                                                                                           |
|                              | *invalid_configuration_platform_services*              | 500    | The platform services configuration is missing or invalid for integration.                                                                                                                                                                                                                                                                 |
|                              | *invalid_configuration_mvpd_platform*                  | 500    | The mvpd platform configuration is missing or invalid for mvpd and platform.                                                                                                                                                                                                                                                               |
|                              | *invalid_configuration_mvpd_platform_boarding_status*  | 500    | The mvpd platform boarding status configuration is missing or invalid for mvpd and platform.                                                                                                                                                                                                                                               |
|                              | *invalid_configuration_mvpd_platform_profile_exchange* | 500    | The mvpd platform profile exchange configuration is missing or invalid for mvpd and platform.                                                                                                                                                                                                                                              |
| **application-registration** | *invalid_access_token_service_provider*                | 401    | The access token is invalid due to invalid service provider.                                                                                                                                                                                                                                                                               |
|                              | *invalid_access_token_client_application*              | 401    | The access token is invalid due to invalid client application.                                                                                                                                                                                                                                                                             |
| **authentication**           | *authenticated_profile_missing*                        | 403    | The authenticated profile associated with this request is missing.                                                                                                                                                                                                                                                                         |
|                              | *authenticated_profile_expired*                        | 403    | The authenticated profile associated with this request has expired.                                                                                                                                                                                                                                                                        |
|                              | *authenticated_profile_invalidated*                    | 403    | The authenticated profile associated with this request has been invalidated.                                                                                                                                                                                                                                                               |
|                              | *temporary_access_duration_limit_exceeded*             | 403    | The temporary access duration limit has been exceeded.                                                                                                                                                                                                                                                                                     |
|                              | *temporary_access_resources_limit_exceeded*            | 403    | The temporary access resources limit has been exceeded.                                                                                                                                                                                                                                                                                    |
|                              | *authorization_denied_by_hba_policies*                 | 403    | The MVPD has returned a "Deny" decision due home-based authentication policies. The current authentication was obtain through a Home-based authentication flow and but the device is no longer in-home when requesting authorization for the specified resource. The user must re-authenticate with a supported MVPD in order to continue. |
|                              | *authorization_denied_by_session_invalidated*          | 403    | The authentication session was invalidated by the identity provider. The user must re-authenticate with a supported MVPD in order to continue.                                                                                                                                                                                             |
|                              | *identity_not_recognized_by_mvpd*                      | 403    | The authorization request failed due to the fact that user identity was not recognized by the MVPD.                                                                                                                                                                                                                                        |
| **retry**                    | *network_received_error*                               | 403    | There was a read error while retrieving the response from the associated partner service. Retrying the request might solve the issue.                                                                                                                                                                                                      |
|                              | *network_connection_timeout*                           | 403    | There was a connection timeout with the associated partner service. Retrying the request might solve the issue.                                                                                                                                                                                                                            |
|                              | *maximum_execution_time_exceeded*                      | 403    | The request did not complete in the maximum allowed time. Retrying the request might solve the issue.                                                                                                                                                                                                                                      |

## Response Handling {#enhanced-error-codes-response-handling}

>[!IMPORTANT]
>
> There are Enhanced Error Codes that can be handled automatically in client application code, such as retrying an authorization request in case of a network timeout or require the user to re-authenticate when their session has expired, but other types might require configuration changes or Adobe Pass Authentication customer care team interaction.
>
> <br/>
>
> Therefore, it is important to collect and provide full error information when creating a ticket through our [Zendesk](https://adobeprimetime.zendesk.com), to ensure that the necessary changes are made before launching the new application or new feature.

In summary, when handling responses containing Enhanced Error Codes, you should consider the following:

1. **Check both status values**: Always check both the HTTP response status code and the Enhanced Error Code "status" field. They might differ, and both provide valuable information.

1. **Agnostic to top-level versus item-level error information**: Handle top-level and item-level error information agnostic to the way it is communicated, ensure you can handle both forms of transmitting Enhanced Error Codes.

1. **Retry logic**: For errors that require a retry, ensure that retries are done with exponential backoff to avoid overwhelming the server. Also, in case of Adobe Pass Authentication APIs that handle multiple items at once (e.g., Preauthorize API), you should include in the repeated request only those items marked with "retry" and not the entire list.

1. **Configuration changes**: For errors that require configuration changes, ensure that the necessary changes are made before launching the new application or new feature.

1. **Authentication and authorization**: For errors related to authentication and authorization, you must prompt the user to re-authenticate or obtain new authorization as needed.

1. **User feedback**: Optional, use the human-readable "message" and (potential) "details" fields to inform the user about the issue. The "details" text message might get passed from the MVPD preauthorization or authorization endpoints or from the Programmer when applying degradation rules.
