---
title: Dynamic Client Registration Flow
description: Dynamic Client Registration Flow
exl-id: d881cf0a-de09-4b1d-a094-d5490f944796
---
# Dynamic Client Registration Flow {#dynamic-client-registration-flow}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Dynamic Client Registration API implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

## Access Adobe Pass protected APIs {#access-adobe-pass-protected-apis}

### Prerequisites {#prerequisites-access-adobe-pass-protected-apis}

Before accessing Adobe Pass protected APIs, ensure the following prerequisites are met:

* A client representative must create a registered application as described in the [Manage registered applications](../dynamic-client-registration-overview.md#manage-registered-applications) section.
* A client representative must download and embed a software statement as described in the [Manage software statements](../dynamic-client-registration-overview.md#manage-software-statements) section.

>[!IMPORTANT]
>
> Adobe Pass Authentication SDKs are responsible for obtaining and refreshing the client credentials and the access token on behalf of the client application.
> 
> For all other Adobe Pass protected APIs, the client application must follow the workflow below.

### Workflow {#workflow-access-adobe-pass-protected-apis}

Follow the given steps to access Adobe Pass protected APIs as shown in the following diagram.

![Access Adobe Pass protected APIs](/help//authentication/assets/dcr-api/dcr-api-access-adobe-pass-protected-apis.png)

*Access Adobe Pass protected APIs*

1. **Retrieve client credentials:** The client application gathers all the necessary data to retrieve client credentials by calling the Client Register endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve client credentials](../apis/dynamic-client-registration-apis-retrieve-client-credentials.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `software_statement`
   > * All the _required_ headers, like `Content-Type`, `X-Device-Info`
   > * All the _optional_ parameters and headers

1. **Return client credentials:** The Client Register endpoint response contains information about the client credentials associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve client credentials](../apis/dynamic-client-registration-apis-retrieve-client-credentials.md#success) API documentation for details on the information provided in a client credentials response.
   >
   > <br/>
   >
   > The Client Register validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Retrieve client credentials](../apis/dynamic-client-registration-apis-retrieve-client-credentials.md#error) API documentation.

   >[!TIP]
   >
   > The client credentials must be cached and used indefinitely.

1. **Retrieve access token:** The client application gathers all the necessary data to retrieve access token by calling the Client Token endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `client_id`, `client_secret`, and `grant_type`
   > * All the _required_ headers, like `Content-Type`, `X-Device-Info`
   > * All the _optional_ parameters and headers

1. **Return access token:** The Client Token endpoint response contains information about the access token associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md#success) API documentation for details on the information provided in an access token response.
   >
   > <br/>
   >
   > The Client Token validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md#error) API documentation.

   >[!TIP]
   >
   > The access token must be cached and used only within the specified duration (e.g., 24-hour time-to-live). After it expires, the client application must request a new access token.

1. **Proceed with accessing protected APIs:** The client application uses the access token to access other Adobe Pass protected APIs. The client application must include the access token in the `Authorization` request header using the `Bearer` authentication scheme (i.e., `Authorization: Bearer <access_token>`).

   >[!IMPORTANT]
   >
   > The Adobe Pass protected APIs validate the access token to ensure that basic conditions are met:
   >
   > * The _access_token_ must be valid.
   > * The _access_token_ must be associated with a valid _client_id_ and _client_secret_.
   > * The _access_token_ must be associated with a valid _software_statement_.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.
