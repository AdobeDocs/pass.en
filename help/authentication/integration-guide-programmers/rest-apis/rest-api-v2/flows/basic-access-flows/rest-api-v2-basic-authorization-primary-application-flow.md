---
title: Basic Authorization - Primary Application - Flow
description: REST API V2 - Basic Authorization - Primary Application - Flow
exl-id: 46bc9326-966e-44fc-8546-2f58be01b7bc
---
# Basic authorization flow performed within primary application {#basic-authorization-flow-performed-within-primary-application}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

The **Authorization flow** within Adobe Pass Authentication entitlement allows the streaming application to determine whether an MVPD permits or denies the user's request to stream content. If the decision is `Permit`, the response includes a media token. Adobe Pass server signs the media token and allows the streaming application to use the media token verifier library to check its authenticity before the stream is released.

The verification with the media token verifier library should occur on the streaming application backend service linked in the chain of permissions for releasing a stream from the CDN.

## Retrieve authorization decisions using specific mvpd {#retrieve-authorization-decisions-using-specific-mvpd}

### Prerequisites {#prerequisites-retrieve-authorization-decisions-using-specific-mvpd}

Before retrieving authorization decisions using a specific MVPD, ensure the following prerequisites are met:

* The streaming application must have a valid regular profile that has been successfully created for the MVPD using one of the basic authentication flows:
  * [Perform authentication within primary application](rest-api-v2-basic-authentication-primary-application-flow.md)
  * [Perform authentication within secondary application with preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
  * [Perform authentication within secondary application without preselected mvpd](rest-api-v2-basic-authentication-secondary-application-flow.md)
* The streaming application must retrieve an authorization decision before playing a user selected resource.

### Workflow {#workflow-retrieve-authorization-decisions-using-specific-mvpd}

Follow the given steps to implement the basic authorization flow using a specific MVPD performed within a primary application as shown in the following diagram.

![Retrieve authorization decisions using specific mvpd](../..//help/authentication/assets/rest-api-v2/flows/basic-access-flows/rest-api-v2-retrieve-authorization-decisions-within-primary-application-using-specific-mvpd.png)

*Retrieve authorization decisions using specific mvpd*

1. **Retrieve authorization decision:** The streaming application gathers all the necessary data to obtain an authorization decision for a specific resource by calling the Decisions Authorize endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authorization decisions using specific mvpd](../../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `resources`
   > * All the _required_ headers, like `Authorization` and `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Find regular profile:** The Adobe Pass server identifies a valid profile based on the received parameters and headers.

1. **Retrieve MVPD decision for requested resource:** The Adobe Pass server calls the MVPD authorization endpoint to obtain a `Permit` or `Deny` decision for the specific resource received from the streaming application.

1. **Return `Permit` decision with media token:** The Decisions Authorize endpoint response contains a `Permit` decision and a media token.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authorization decisions using specific mvpd](../../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) API documentation for details on the information provided in a decision response.
   > 
   > <br/>
   > 
   > The Decisions Authorize endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Start stream with media token:** The streaming application uses the media token to play the content.

1. **Return `Deny` decision with details:** The Decisions Authorize endpoint response contains a `Deny` decision and an error payload which adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authorization decisions using specific mvpd](../../apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) API documentation for details on the information provided in a decision response.
   > 
   > <br/>
   > 
   > The Decisions Authorize endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.

1. **Handle `Deny` decision details:** The streaming application processes the error information from the response and can use it to optionally display a specific message on the user interface.
