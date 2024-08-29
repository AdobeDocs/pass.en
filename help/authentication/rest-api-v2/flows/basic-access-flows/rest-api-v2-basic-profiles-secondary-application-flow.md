---
title: Basic Profiles - Secondary Application - Flow
description: REST API V2 - Basic Profiles - Secondary Application - Flow
exl-id: 1fcefcfa-7534-4b85-b3b5-df513685d66b
---
# Basic profiles flow performed within secondary application {#basic-profiles-flow-secondary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

The **Profiles flow** within Adobe Pass Authentication entitlement allows the secondary application to access information on active user logins.

Basic profiles flow allows you to query for the following scenarios:

* [Retrieve profile for specific code](#retrieve-profile-for-specific-code)

## Retrieve profile for specific code {#retrieve-profile-for-specific-code}

### Prerequisites {#prerequisites-retrieve-profile-for-specific-code}

Before retrieving the profile for a specific authentication code, ensure the following prerequisites are met:

* The secondary application, which has a `code` used to perform the interactive authentication with the MVPD, wants to retrieve the profile for a specific authentication code.

### Workflow {#workflow-retrieve-profile-for-specific-code}

Follow the given steps to implement the basic profile retrieval flow for a specific authentication code performed within a secondary application as shown in the following diagram.

![Retrieve profile for specific code](../../../assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-profile-within-secondary-application-for-specific-code.png)

*Retrieve profile for specific code*

1. **Retrieve profile for specific code:** The secondary application gathers all the necessary data to retrieve profile information for that specific authentication code by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific code](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, and `code`
   > * All the _required_ headers, like `Authorization`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Return information about regular profile:** The Profiles endpoint response contains information about the found profile associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific code](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) API documentation for details on the information provided in a profile response.
   > 
   > <br/>
   > 
   > The Profiles endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

1. **Indicate authentication flow finished with success:** If the Profiles endpoint response contains a profile, the secondary application processes the response and can use it to optionally display a specific message on the user interface.

1. **Indicate authentication flow encountered a problem:** If the Profiles endpoint response does not contain a profile, the secondary application processes the response and can use it to optionally display a specific message on the user interface.
