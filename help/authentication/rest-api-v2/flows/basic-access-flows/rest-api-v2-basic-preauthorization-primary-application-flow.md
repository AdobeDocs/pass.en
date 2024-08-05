---
title: Basic Preauthorization - Primary Application - Flow
description: REST API V2 - Basic Preauthorization - Primary Application - Flow
---

# Basic preauthorization flow performed within primary application {#basic-preauthorization-flow-performed-within-primary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/throttling-mechanism.md) documentation.

The **Preauthorization flow** within Adobe Pass Authentication entitlement allows the streaming application to determine whether an MVPD may permit or deny the user's access to a list of resources. This verification ensures the application can present accurate information to the user about the content they might be eligible to view.

## Retrieve preauthorization decisions using specific mvpd {#retrieve-preauthorization-decisions-using-specific-mvpd}

### Prerequisites {#prerequisites-retrieve-preauthorization-decisions-using-specific-mvpd}

Before retrieving preauthorization decisions using a specific MVPD, ensure the following prerequisites are met:

* The streaming application must have a valid regular profile that has been successfully created for the MVPD using one of the basic authentication flows:
   * [Perform authentication within primary application](./rest-api-v2-basic-authentication-primary-application-flow.md)
   * [Perform authentication within secondary application with preselected mvpd](./rest-api-v2-basic-authentication-secondary-application-flow.md)
   * [Perform authentication within secondary application without preselected mvpd](./rest-api-v2-basic-authentication-secondary-application-flow.md)
* The streaming application wants to retrieve preauthorization decisions to display a list of resources along with their associated statuses.

### Workflow {#workflow-retrieve-preauthorization-decisions-using-specific-mvpd}

Follow the given steps to implement the basic preauthorization flow using a specific MVPD performed within a primary application as shown in the following diagram.

![Retrieve preauthorization decisions using specific mvpd](../../../assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-preauthorization-decisions-within-primary-application-using-specific-mvpd.png)

*Retrieve preauthorization decisions using specific mvpd*

1. **Retrieve preauthorization decisions:** The streaming application gathers all the necessary data to obtain preauthorization decisions for a list of resources by calling the Decisions Preauthorize endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve preauthorization decisions using specific mvpd](../../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `resources`
   > * All the _required_ headers, like `Authorization` and `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Retrieve MVPD decisions for requested resources:** The Adobe Pass server calls the MVPD preauthorization endpoint to obtain a `Permit` or `Deny` decision for each resource received from the streaming application.

1. **Return preauthorization decisions:** The Decisions Preauthorize endpoint response contains a `Permit` or `Deny` decision for each resource:
    * A `Permit` decision means the resource is playable. The response does not include a media token, as the preauthorization flow must not be used to play resources.
    * A `Deny` decision means the resource is not playable. The response includes an error payload which adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve preauthorization decisions using specific mvpd](../../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) API documentation for details on the information provided in a decision response.
   > 
   > <br/>
   > 
   > The Decisions Preauthorize endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../enhanced-error-codes.md) documentation.

1. **Handle preauthorization decisions:** The streaming application processes the response and can use it to optionally display the appropriate status for each resource on the user interface.
