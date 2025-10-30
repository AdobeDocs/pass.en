---
title: Single Logout - Flow
description: REST API V2 - Single Logout - Flow
exl-id: d7092ca7-ea7b-4e92-b45f-e373a6d673d6
---
# Single logout flow {#single-logout-flow}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

>[!MORELIKETHIS]
>
> Make sure to also visit the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general).

## Initiate single logout for specific mvpd {#initiate-single-logout-for-specific-mvpd}

### Prerequisites {#prerequisites-initiate-single-logout-for-specific-mvpd}

Before initiating single logout for a specific MVPD, ensure the following prerequisites are met:

* The second streaming application must have a valid single sign-on profile that has been successfully created for the MVPD using one of the single sign-on authentication flows:
    * [Perform authentication through single sign-on using platform identity](rest-api-v2-single-sign-on-platform-identity-flows.md)
    * [Perform authentication through single sign-on using service token](rest-api-v2-single-sign-on-service-token-flows.md)
* The second streaming application must initiate the single logout flow when it needs to sign out of the MVPD.

>[!IMPORTANT]
> 
> Assumptions
>
> <br/>
> 
> * The first and second streaming applications obtain the same unique platform identifier payload as `JWS` or `JWE` or the same unique user identifier payload as `JWS`.

### Workflow {#workflow-initiate-single-logout-for-specific-mvpd}

Perform the given steps to implement the single logout flow for a specific MVPD as shown in the following diagram.

![Initiate single logout for specific mvpd](../..//help/authentication/assets/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-initiate-single-logout-for-specific-mvpd-flow.png)

*Initiate single logout for specific mvpd*

1. **Initiate Adobe Pass logout:** The streaming application gathers all the necessary data to initiate the logout flow by calling the Adobe Pass Logout endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](../../apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the unique platform identifier or the unique user identifier before making a request.
   >
   > <br/>
   > 
   > For more details about `Adobe-Subject-Token` header, refer to the [Adobe-Subject-Token](../../appendix/headers/rest-api-v2-appendix-headers-adobe-subject-token.md) documentation.
   > 
   > <br/> 
   > 
   > For more details about `AD-Service-Token` header, refer to the [AD-Service-Token](../../appendix/headers/rest-api-v2-appendix-headers-ad-service-token.md) documentation.

1. **Find regular and single sign-on profiles:** The Adobe Pass server identifies both regular and single sign-on valid profiles based on the received parameters and headers.

1. **Delete regular and single sign-on profiles:** The Adobe Pass server deletes the identified regular and single sign-on profiles from the Adobe Pass backend.

1. **Indicate the next action:** The Adobe Pass Logout endpoint response contains the necessary data to guide the streaming application regarding the next action.

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

1. **Indicate logout complete:** If the MVPD does not support the logout flow, the streaming application processes the response and can use it to optionally display a specific message on the user interface.

1. **Initiate MVPD logout:** If the MVPD does support the logout flow, the streaming application processes the response and uses a user agent to initiate the logout flow with the MVPD. The flow may include several redirects to MVPD systems. Still, the result is that the MVPD performs its internal cleanup and sends the final logout confirmation back to the Adobe Pass backend.

1. **Indicate logout complete:** The streaming application can wait for the user agent to reach the provided `redirectUrl` and can use it as a signal to optionally display a specific message on the user interface.

>[!NOTE]
>
> The steps for the single logout flow are the same as above, if initiated from the first streaming application.
