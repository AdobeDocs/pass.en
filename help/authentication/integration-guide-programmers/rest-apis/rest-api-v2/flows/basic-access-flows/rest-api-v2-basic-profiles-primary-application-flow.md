---
title: Basic Profiles - Primary Application - Flow
description: REST API V2 - Basic Profiles - Primary Application - Flow
exl-id: 19ddf382-9a32-4b94-aa84-7611c0e1780e
---
# Basic profiles flow performed within primary application {#basic-profiles-flow-primary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

>[!MORELIKETHIS]
>
> Make sure to also visit the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general).

The **Profiles flow** within Adobe Pass Authentication entitlement allows the streaming application to access information on active user logins.

Basic profiles flow allows you to query for the following scenarios:

* [Retrieve profiles](#retrieve-profiles)
* [Retrieve profile for specific mvpd](#retrieve-profile-for-specific-mvpd)
* [Retrieve profile for specific code](#retrieve-profile-for-specific-code)

## Retrieve profiles {#retrieve-profiles}

### Prerequisites {#prerequisites-retrieve-profiles}

Before retrieving profiles, ensure the following prerequisites are met:

* The streaming application wants to retrieve all regular profiles.

### Workflow {#workflow-retrieve-profiles}

Follow the given steps to implement the basic profiles retrieval flow performed within a primary application as shown in the following diagram.

![Retrieve profiles](/help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-profiles-within-primary-application.png)

*Retrieve profiles*

1. **Retrieve profiles:** The streaming application gathers all the necessary data to retrieve all profiles information by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profiles](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profiles:** The Adobe Pass server identifies all valid profiles based on the received parameters and headers.

1. **Return information about regular profiles:** The Profiles endpoint response contains information about the found profiles associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profiles](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) API documentation for details on the information provided in a profile response.
   > 
   > <br/>
   > 
   > The Profiles endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Choose a profile and proceed with decisions flows:** If the Profiles endpoint response contains profiles, the streaming application uses its internal logic (eventually by interacting with the end user) to choose one of the available profiles to continue with subsequent decisions flows.

1. **Indicate new basic authentication flow:** If the Profiles endpoint response does not contain a profile, the streaming application indicates the user to initiate a new basic authentication flow.

## Retrieve profile for specific mvpd {#retrieve-profile-for-specific-mvpd}

### Prerequisites {#prerequisites-retrieve-profile-for-specific-mvpd}

Before retrieving the profile for a specific MVPD, ensure the following prerequisites are met:

* The streaming application, which has a selected or cached `mvpd` identifier, wants to retrieve the regular profile for a specific MVPD.

### Workflow {#workflow-retrieve-profile-for-specific-mvpd}

Follow the given steps to implement the basic profile retrieval flow for a specific MVPD performed within a primary application as shown in the following diagram.

![Retrieve profile for specific mvpd](/help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-profile-within-primary-application-for-specific-mvpd.png)

*Retrieve profile for specific mvpd*

1. **Retrieve profile for specific mvpd:** The streaming application gathers all the necessary data to retrieve profile information for that specific MVPD by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific mvpd](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `mvpd`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Return information about regular profile:** The Profiles endpoint response contains information about the found profile associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific mvpd](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) API documentation for details on the information provided in a profile response.
   > 
   > <br/>
   > 
   > The Profiles endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Proceed with decisions flows:** If the Profiles endpoint response contains a profile, the streaming application uses the profile information to continue with subsequent decisions flows.

1. **Indicate new basic authentication flow:** If the Profiles endpoint response does not contain a profile, the streaming application indicates the user to initiate a new basic authentication flow.

## Retrieve profile for specific code {#retrieve-profile-for-specific-code}

### Prerequisites {#prerequisites-retrieve-profile-for-specific-code}

Before retrieving the profile for a specific authentication code, ensure the following prerequisites are met:

* The streaming application, which has a `code` used to perform the interactive authentication with the MVPD, wants to retrieve the profile for a specific authentication code.

### Workflow {#workflow-retrieve-profile-for-specific-code}

Follow the given steps to implement the basic profile retrieval flow for a specific authentication code performed within a primary application as shown in the following diagram.

![Retrieve profile for specific code](/help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-profile-within-primary-application-for-specific-code.png)

*Retrieve profile for specific code*

1. **Retrieve profile for specific code:** The streaming application gathers all the necessary data to retrieve profile information for that specific authentication code by sending a request to the Profiles endpoint.

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
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Proceed with decisions flows:** If the Profiles endpoint response contains a profile, the streaming application uses the profile information to continue with subsequent decisions flows.

1. **Indicate new basic authentication flow:** If the Profiles endpoint response does not contain a profile, the primary application indicates the user to initiate a new basic authentication flow.
