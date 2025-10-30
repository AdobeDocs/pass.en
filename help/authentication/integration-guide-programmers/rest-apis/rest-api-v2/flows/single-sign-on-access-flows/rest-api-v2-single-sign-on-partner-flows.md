---
title: Single Sign-On - Partner - Flows
description: REST API V2 - Single Sign-On - Partner - Flows
exl-id: 5735d67f-a311-4d03-ad48-93c0fcbcace5
---
# Single sign-on using partner flows {#single-sign-on-partner-flows}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

>[!MORELIKETHIS]
>
> Make sure to also visit the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general).

The Partner method enables multiple applications to use a partner framework status payload to achieve single sign-on (SSO) at the device level when using Adobe Pass services.

The applications are responsible for retrieving the partner framework status payload using partner specific frameworks or libraries outside of Adobe Pass systems.

The applications are responsible for including this partner framework status payload as part of the `AP-Partner-Framework-Status` header for all requests that specify it.

For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

The Adobe Pass Authentication REST API V2 has support for Partner Single Sign-On (SSO) for end users of client applications running on iOS, iPadOS or tvOS.

For more details about single sign-on (SSO) for Apple platform, refer to the [Apple SSO Cookbook (REST API V2)](/help/premium-workflow/sso-access/partner-sso/apple-sso/apple-sso-cookbook-rest-api-v2.md) documentation.

## Retrieve partner authentication request {#retrieve-partner-authentication-request}

### Prerequisites {#prerequisites-retrieve-partner-authentication-request}

Before retrieving the partner authentication request, ensure the following prerequisites are met:

* The partner framework must select an MVPD.
* The streaming application must obtain the partner framework status information from the partner framework and pass it to the Adobe Pass server.
* The streaming application must obtain the partner authentication request from the Adobe Pass server and pass it to the partner framework.

>[!IMPORTANT]
>
> Assumptions
> 
> <br/>
> 
> * The partner framework supports user interaction to select an MVPD.
> * The partner framework supports user interaction to authenticate with the selected MVPD.
> * The partner framework provides user permission and provider information.

### Workflow {#workflow-retrieve-partner-authentication-request}

Perform the given steps to retrieve the partner authentication request as shown in the following diagram.

![Retrieve partner authentication request](/help/authentication/assets/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-retrieve-partner-authentication-request-flow.png)

*Retrieve partner authentication request*

1. **Retrieve partner framework status:** The streaming application calls the partner framework, outside of Adobe Pass systems, to obtain user permission and provider information.

1. **Return partner framework status information:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Retrieve partner authentication request:** The streaming application gathers all the necessary data to initiate an authentication session by calling the Sessions Partner endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve partner authentication request](../../apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `partner`
   > * All the _required_ headers like `Authorization`, `AP-Device-Identifier`, `Content-Type`, `X-Device-Info`, and `AP-Partner-Framework-Status`
   > * All the _optional_ headers and parameters
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request.
   >
   > <br/>
   > 
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Indicate the next action:** The Sessions Partner endpoint response contains the necessary data to guide the streaming application regarding the next action.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve partner authentication request](../../apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md) API documentation for details on the information provided in a session response.
   > 
   > <br/>
   > 
   > The Sessions Partner endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If basic validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.
   >
   > <br/>
   >
   > The Sessions Partner endpoint validates the request data to ensure that partner single sign-on conditions are met:
   >
   >  * The partner single sign-on configuration in the Adobe Pass server must be valid and enabled.
   >  * The partner framework status payload received via the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) header must be valid.
   >
   > <br/>
   >
   > If partner single sign-on validation fails, the response will default to the basic authentication flow.

1. **Proceed with profile retrieval flow using partner authentication response:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to "partner_profile".
   * The `actionType` attribute is set to "direct".
   * The `authenticationRequest - type` attribute includes the security protocol used by the partner framework for MVPD login (currently set to SAML only).
   * The `authenticationRequest - request` attribute includes the SAML request that is passed to the partner framework.
   * The `authenticationRequest - attributesNames` attribute includes the SAML attributes that are passed to the partner framework.

   If the Adobe Pass backend does not identify a valid profile and the partner single sign-on validation passes, the streaming application receives a response with actions and data to pass to the partner framework for starting the authentication flow with the MVPD.

   For more details about the profile retrieval flow using a partner authentication response, refer to the [Crreate and retrieve profile using partner authentication response](#create-and-retrieve-profile-using-partner-authentication-response) section.

1. **Proceed with basic authentication flow:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to either "authenticate" or "resume".
   * The `actionType` attribute is set to either "interactive" or "direct".

   If the Adobe Pass backend does not identify a valid profile and the partner single sign-on validation fails, the Adobe Pass server falls back to the basic authentication flow.

   For more details about the basic authentication flow, refer to the following documents:
   * [Perform authentication within primary application](../basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
   * [Perform authentication within secondary application with preselected mvpd](../basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
   * [Perform authentication within secondary application without preselected mvpd](../basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)

1. **Proceed with decisions flows:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to "authorize".
   * The `actionType` attribute is set to "direct".

   If the Adobe Pass backend identifies a valid profile, the streaming application does not need to re-authenticate with the selected MVPD, as there is already a profile that can be used for subsequent decisions flows.

   >[!IMPORTANT]
   >
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request.
   >
   > <br/>
   > 
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

## Create and retrieve profile using partner authentication response {#create-and-retrieve-profile-using-partner-authentication-response}

### Prerequisites {#prerequisites-create-and-retrieve-profile-using-partner-authentication-response}

Before retrieving the profile using a partner authentication response, ensure the following prerequisites are met:

* The partner framework must perform authentication with the selected MVPD.
* The streaming application must obtain the partner authentication response along with partner framework status information from the partner framework and pass it to the Adobe Pass server.

>[!IMPORTANT]
>
> Assumption
>
> * The partner framework supports user interaction to select an MVPD.
> * The partner framework supports user interaction to authenticate with the selected MVPD.
> * The partner framework provides user permission and provider information.

### Workflow {#workflow-create-and-retrieve-profile-using-partner-authentication-response}

Perform the given steps to implement the profile retrieval flow using a partner authentication response as shown in the following diagram.

![Create and retrieve profile using partner authentication response](/help/authentication/assets/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-retrieve-profile-using-partner-authentication-response-flow.png)

*Create and retrieve authenticated profile using partner authentication response*

1. **Complete MVPD authentication with partner framework:** If the authentication flow is successful, the partner framework interaction with the MVPD produces a partner authentication response (SAML response) that is returned along with the partner framework status information.

1. **Return partner authentication response:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Create and retrieve profile using partner authentication response:** The streaming application gathers all the necessary data to create and retrieve a profile by calling the Profiles Partner endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Create and retrieve profile using partner authentication response](../../apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `partner`, and `SAMLResponse`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`, `Content-Type`, `X-Device-Info`, and `AP-Partner-Framework-Status`
   > * All the _optional_ headers and parameters
   >
   > <br/>
   > 
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request.
   >
   > <br/>
   > 
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Create and save partner profile:** The Adobe Pass server creates and saves a partner profile after ensuring that all conditions are met.

1. **Return information about partner profile:** The Profiles endpoint response contains information about the partner profile, including the attribute `type` set to "appleSSO".

   >[!IMPORTANT]
   >
   > Refer to the [Create and retrieve profile using partner authentication response](../../apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md) API documentation for details on the information provided in a profile response.
   > 
   > <br/>
   > 
   > The Profiles Partner endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   > * The integration between the provided `serviceProvider` and `mvpd` must be active.
   >
   > <br/>
   > 
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](../../../../features-standard/error-reporting/enhanced-error-codes.md) documentation.
   >
   > <br/>
   >
   > The Profiles Partner endpoint validates the request data to ensure that partner single sign-on conditions are met:
   >
   >  * The partner single sign-on configuration in the Adobe Pass server must be valid and enabled.
   >  * The partner framework status payload received via the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) header must be valid.
   >
   > <br/>
   >
   > If partner single sign-on validation fails, the response will default to the basic profile retrieval flow.

1. **Proceed with decisions flows:** The streaming application can continue with subsequent decisions flows.

   >[!IMPORTANT]
   >
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request.
   >
   > <br/>
   > 
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](../../appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.
