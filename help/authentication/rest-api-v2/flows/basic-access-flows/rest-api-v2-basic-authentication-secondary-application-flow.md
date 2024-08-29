---
title: Basic Authentication - Secondary Application - Flow
description: REST API V2 - Basic Authentication - Secondary Application - Flow
exl-id: 83bf592e-c679-4cfe-984d-710a9598c620
---
# Basic authentication flow performed within secondary application {#basic-authentication-flow-performed-within-secondary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

The **Authentication flow** within Adobe Pass Authentication entitlement allows the streaming application to verify that a user has a valid MVPD account. This process requires the user to have an active MVPD account and enter valid login credentials on the MVPD login page.

Authentication flow is required in the following cases:

* When the user opens an application for the first time.
* When the user's previous authentication has expired.
* When the user logs out from the MVPD account.
* When the user wants to authenticate with a different MVPD.

In all of these cases, the application calling any of the Profiles endpoints receives an empty response or one or more profiles, but for different MVPDs.

The **Authentication flow** requires a user agent (browser) to complete a series of calls from the application to Adobe Pass backend, then to the MVPD login page, and finally back to the application. This flow may include several redirects to MVPD systems and managing cookies or sessions stored for each domain, which can be challenging to achieve and secure without a user agent.

Based on the primary application (streaming application) capabilities to support user interaction to select an MVPD and to authenticate with the selected MVPD in a user agent, the authentication scenarios are:

* [Perform authentication within primary application](./rest-api-v2-basic-authentication-primary-application-flow.md)
* [Perform authentication within secondary application with preselected mvpd](./rest-api-v2-basic-authentication-secondary-application-flow.md)
* [Perform authentication within secondary application without preselected mvpd](./rest-api-v2-basic-authentication-secondary-application-flow.md)

## Perform authentication within secondary application with preselected mvpd {#perform-authentication-within-secondary-application-with-preselected-mvpd}

### Prerequisites {#prerequisites-perform-authentication-within-secondary-application-with-preselected-mvpd}

Before starting the authentication flow within a primary application and finishing it through user interaction within a secondary application, ensure the following prerequisites are met:

* The streaming application must select an MVPD.
* The streaming application must initiate an authentication session to sign in with the selected MVPD.
* The secondary application must authenticate with the selected MVPD in a user agent.

>[!IMPORTANT]
>
> Assumptions
>
> <br/>
> 
> * The streaming application supports user interaction to select an MVPD.
> * The secondary application (usually on a secondary device) supports user interaction to authenticate with the selected MVPD in a user agent.

### Workflow {#workflow-perform-authentication-within-secondary-application-with-preselected-mvpd}

Follow the given steps to implement the basic authentication flow performed within a secondary application with a preselected MVPD as shown in the following diagram.

![Perform authentication within secondary application with preselected mvpd](../../../assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-perform-authentication-within-secondary-application-with-preselected-mvpd.png)

*Perform authentication within secondary application with preselected mvpd*

1. **Create authentication session:** The streaming application gathers all the necessary data to initiate an authentication session by calling the Sessions endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Create authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) API documentation for details on:
   > 
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, `domainName`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   > 
   > The streaming application must provide all the required parameters in a single call when creating the authentication session.

1. **Indicate the next action:** The Sessions endpoint response contains the necessary data to guide the streaming application regarding the next action.

   >[!IMPORTANT]
   >
   > Refer to the [Create authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) API documentation for details on the information provided in a session response.
   > 
   > <br/>
   > 
   > The Sessions endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

1. **Proceed with decisions flows:** The Sessions endpoint response contains the following data:
   * The `actionName` attribute is set to "authorize".
   * The `actionType` attribute is set to "direct".

   If the Adobe Pass backend identifies a valid profile, the streaming application does not need to re-authenticate with the selected MVPD, as there is already a profile that can be used for subsequent decisions flows.

1. **Display authentication code:** The Sessions endpoint response contains the following data:
   * The `code` which can be used to resume the authentication session within a secondary application.
   * The `actionName` attribute is set to "authenticate".
   * The `actionType` attribute is set to "interactive".

   If the Adobe Pass backend does not identify a valid profile, the streaming application displays the `code` that can be used to resume the authentication session within a secondary application.

1. **Validate authentication code:** The secondary application validates the user provided `code` to ensure it can proceed with MVPD authentication in user agent. 

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authentication session information](../../apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `code`
   > * All the _required_ headers, like `Authorization`
   > * All the _optional_ parameters and headers

1. **Return information about authentication session:** The Sessions endpoint response contains the following data:
   * The `existing` attribute contains the existing parameters that were already provided.
   * The `missing` attribute contains the missing parameters that need to be provided in order to complete the authentication flow.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authentication session information](../../apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md) API documentation for details on the information provided in a session validation response.
   >
   > <br/>
   >
   > The Sessions endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

   >[!NOTE]
   >
   > Suggestion: The secondary application can inform users that the `code` used is invalid in the event of an error response indicating a missing authentication session, and advise them to retry using a new one.
   
1. **Open URL in user agent:** The secondary application opens a user agent to load the self computed `url`, making a request to the Authenticate endpoint. This flow may include several redirects, ultimately leading the user to the MVPD login page and provide valid credentials.

   >[!IMPORTANT]
   >
   > Refer to the [Perform authentication in user agent](../../apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `code`
   > * All the _optional_ parameters and headers

1. **Complete MVPD authentication:** If the authentication flow is successful, the user agent interaction saves a regular profile in Adobe Pass backend and reaches the provided `redirectUrl`.

1. **Retrieve profile for specific code:** The streaming application gathers all the necessary data to retrieve profile information by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific code](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) API documentation for details on:
   > 
   > * All the _required_ parameters, like `serviceProvider` and `code`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

   >[!NOTE]
   >
   > Suggestion: The streaming application can implement a polling mechanism using the `code` to check if the regular profile was successfully generated and saved.

1. **Return information about regular profile:** The Profiles endpoint response contains information about the regular profile associated with the received parameters and headers.

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

## Perform authentication within secondary application without preselected mvpd {#perform-authentication-within-secondary-application-without-preselected-mvpd}

### Prerequisites {#prerequisites-perform-authentication-within-secondary-application-without-preselected-mvpd}

Before starting the authentication flow within a primary application and finishing it through user interaction within a secondary application, ensure the following prerequisites are met:

* The streaming application must initiate an authentication session when it needs to sign in.
* The secondary application must select an MVPD.
* The secondary application must authenticate with the selected MVPD in a user agent.

>[!IMPORTANT]
>
> Assumptions
>
> <br/>
> 
> * The secondary application (usually on a secondary device) supports user interaction to select an MVPD.
> * The secondary application (usually on a secondary device) supports user interaction to authenticate with the selected MVPD in a user agent.

### Workflow {#workflow-perform-authentication-within-secondary-application-without-preselected-mvpd}

Follow the given steps to implement the basic authentication flow performed within a secondary application without a preselected MVPD as shown in the following diagram.

![Perform authentication within secondary application without preselected mvpd](../../../assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-perform-authentication-within-secondary-application-without-preselected-mvpd.png)

*Perform authentication within secondary application without preselected mvpd*

1. **Create authentication session:** The streaming application gathers some of the necessary data to initiate an authentication session by calling the Sessions endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Create authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   > 
   > The streaming application cannot provide all the required parameters in a single call when creating the authentication session.

1. **Indicate the next action:** The Sessions endpoint response contains the necessary data to guide the streaming application regarding the next action:
   * The `code` which can be used to resume the authentication session within a secondary application.
   * The `actionName` attribute is set to "resume".
   * The `actionType` attribute is set to "direct".

   >[!IMPORTANT]
   >
   > Refer to the [Create authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) API documentation for details on the information provided in a session response.
   > 
   > <br/>
   > 
   > The Sessions endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

1. **Display authentication code:** The streaming application displays the `code` that can be used to resume the authentication session within a secondary application.

1. **Provide authentication session missing parameters:** The secondary application gathers all the missing data required to resume the authentication session and calls the Sessions endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Resume authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, `domainName`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Indicate the next action:** The Sessions endpoint response contains the necessary data to guide the streaming application regarding the next action.

   >[!IMPORTANT]
   >
   > Refer to the [Resume authentication session](../../apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) API documentation for details on the information provided in a session response.
   > 
   > <br/>
   > 
   > The Sessions endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

   >[!NOTE]
   >
   > Suggestion: The secondary application can inform users that the `code` used is invalid in the event of an error response indicating a missing authentication session, and advise them to retry using a new one.

1. **Indicate existing profile:** The Sessions endpoint response contains the following data:
   * The `actionName` attribute is set to "authorize".
   * The `actionType` attribute is set to "direct".

   If the Adobe Pass backend identifies a valid profile, the streaming application does not need to re-authenticate with the selected MVPD, as there is already a profile that can be used for subsequent decisions flows.

1. **Open URL in user agent:** The Sessions endpoint response contains the following data:
   * The `url` which can be used to initiate the interactive authentication within the MVPD login page.
   * The `actionName` attribute is set to "authenticate".
   * The `actionType` attribute is set to "interactive".

   If the Adobe Pass backend does not identify a valid profile, the secondary application opens a user agent to load the provided `url`, making a request to the Authenticate endpoint. This flow may include several redirects, ultimately leading the user to the MVPD login page and provide valid credentials.

1. **Complete MVPD authentication:** If the authentication flow is successful, the user agent interaction saves a regular profile in the Adobe Pass backend and reaches the provided `redirectUrl`.

1. **Retrieve profile for specific code:** The streaming application gathers all the necessary data to retrieve profile information by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile for specific code](../../apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `code`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

   >[!NOTE]
   >
   > Suggestion: The streaming application can implement a polling mechanism using the `code` to check if the regular profile was successfully generated and saved.

1. **Return information about regular profile:** The Profiles endpoint response contains information about the regular profile associated with the received parameters and headers.

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
