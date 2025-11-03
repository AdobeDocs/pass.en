---
title: Basic Logout - Primary Application - Flow
description: REST API V2 - Basic Logout - Primary Application - Flow
exl-id: 21dbff4a-0d69-4f81-b04f-e99d743c35b3
---
# Basic logout flow performed within primary application {#basic-logout-flow-performed-within-primary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

The **Logout flow** within Adobe Pass Authentication entitlement allows the streaming application to perform two main steps:

* Delete the regular profiles saved on the Adobe Pass backend.
* Use a user agent (browser) to navigate to the MVPD logout endpoint, triggering a cleanup on the MVPD backend.

Basic logout flow allows you to query for the following scenarios:

* [Initiate logout for specific mvpd with logout endpoint](#initiate-logout-for-specific-mvpd-with-logout-endpoint)
* [Initiate logout for specific mvpd without logout endpoint](#initiate-logout-for-specific-mvpd-without-logout-endpoint)

## Initiate logout for specific mvpd having logout endpoint {#initiate-logout-for-specific-mvpd-with-logout-endpoint}

### Prerequisites {#prerequisites-initiate-logout-for-specific-mvpd-with-logout-endpoint}

Before initiating logout for a specific MVPD with a logout endpoint, ensure the following prerequisites are met:

* The streaming application must have a valid regular profile that has been successfully created for the MVPD using one of the basic authentication flows:
   * [Perform authentication within primary application](rest-api-v2-basic-authentication-primary-application-flow.md)
   * [Perform authentication within secondary application with preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
   * [Perform authentication within secondary application without preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
* The streaming application must initiate the logout flow when it needs to sign out of the MVPD.

>[!IMPORTANT]
>
> Assumptions
>
> <br/>
> 
> * The MVPD supports the logout flow and has a logout endpoint.

### Workflow {#workflow-initiate-logout-for-specific-mvpd-with-logout-endpoint}

Follow the given steps to implement the basic logout flow for a specific MVPD with a logout endpoint performed within a primary application as shown in the following diagram.

![Initiate logout for specific mvpd with logout endpoint](/help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-initiate-logout-within-primary-application-for-specific-mvpd-with-logout-endpoint.png)

*Initiate logout for specific mvpd with logout endpoint*

1. **Initiate Adobe Pass logout:** The streaming application gathers all the necessary data to initiate the logout flow by calling the Adobe Pass Logout endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](../../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Delete regular profile:** The Adobe Pass server deletes the identified regular profile from the Adobe Pass backend.

1. **Indicate the next action:** The Adobe Pass Logout endpoint response contains the necessary data to guide the streaming application regarding the next action:
   * The `url` attribute is present since the MVPD supports the logout flow.
   * The `actionName` attribute is set to "logout".
   * The `actionType` attribute is set to "interactive".

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](../../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) API documentation for details on the information provided in a logout response.
   > 
   > <br/>
   > 
   > The Adobe Pass Logout endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Initiate MVPD logout:** The streaming application reads the `url` and uses a user agent to initiate the logout flow with the MVPD. The flow may include several redirects to MVPD systems. Still, the result is that the MVPD performs its internal cleanup and sends the final logout confirmation back to the Adobe Pass backend.

1. **Indicate logout complete:** The streaming application can wait for the user agent to reach the provided `redirectUrl` and can use it as a signal to optionally display a specific message on the user interface.

## Initiate logout for specific mvpd without logout endpoint {#initiate-logout-for-specific-mvpd-without-logout-endpoint}

### Prerequisites {#prerequisites-initiate-logout-for-specific-mvpd-without-logout-endpoint}

Before initiating logout for a specific MVPD without a logout endpoint, ensure the following prerequisites are met:

* The streaming application must have a valid regular profile that has been successfully created for the MVPD using one of the basic authentication flows:
   * [Perform authentication within primary application](rest-api-v2-basic-authentication-primary-application-flow.md)
   * [Perform authentication within secondary application with preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
   * [Perform authentication within secondary application without preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
* The streaming application must initiate the logout flow when it needs to sign out of the MVPD.

>[!IMPORTANT]
>
> Assumptions
>
> <br/>
> 
> * The MVPD does not support the logout flow and does not have a logout endpoint.

### Workflow {#workflow-initiate-logout-for-specific-mvpd-without-logout-endpoint}

Follow the given steps to implement the basic logout flow for a specific MVPD without a logout endpoint performed within a primary application as shown in the following diagram.

![Initiate logout for specific mvpd without logout endpoint](/help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-initiate-logout-within-primary-application-for-specific-mvpd-without-logout-endpoint.png)

*Initiate logout for specific mvpd without logout endpoint*

1. **Initiate Adobe Pass logout:** The streaming application gathers all the necessary data to initiate the logout flow by calling the Adobe Pass Logout endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](../../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Delete regular profile:** The Adobe Pass server deletes the identified regular profile.

1. **Indicate the next action:** The Adobe Pass Logout endpoint response contains the necessary data to guide the streaming application regarding the next action:
   * The `url` attribute is missing since the MVPD does not support the logout flow.
   * The `actionName` attribute is set to "complete".
   * The `actionType` attribute is set to "none".

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](../../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) API documentation for details on the information provided in a logout response.
   > 
   > <br/>
   > 
   > The Adobe Pass Logout endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Indicate logout complete:** The streaming application processes the response and can use it to optionally display a specific message on the user interface.
