---
title: Apple SSO Cookbook (REST API V2)
description: Apple SSO Cookbook (REST API V2)
exl-id: 81476312-9ba4-47a0-a4f7-9a557608cfd6
---
# Apple SSO Cookbook (REST API V2) {#apple-sso-cookbook-rest-api-v2}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The Adobe Pass Authentication REST API V2 has support for Partner Single Sign-On (SSO) for end users of client applications running on iOS, iPadOS or tvOS.

This document acts as an extension to the existing REST API V2 documentation that describes how to implement [Single sign-on using partner flows](/help/authentication/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-partner-flows.md).

## Apple single sign-on using partner flows {#apple-sso-cookbook-rest-api-v2-cookbook}

### Prerequisites {#apple-sso-cookbook-rest-api-v2-prerequisites}

Before proceeding with the Apple single sign-on using partner flows, ensure the following prerequisites are met:

* The streaming application must gather all the necessary data required by the `X-Device-Info` and/or `User-Agent` headers such that the Adobe Pass Authentication backend can identify the device platform and its capabilities. For more details about `X-Device-Info` header, refer to the [X-Device-Info](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) documentation.

* The streaming application must request access to the user's subscription information saved at device level, for which the user must give the application permission to proceed, similar to providing access to the device's camera or microphone. This permission must be requested per application using Apple's [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) and the device will save the user's selection.
   
  We recommend incentivizing users who refuse to give permission to access subscription information by explaining the benefits of the Apple single sign-on user experience, but be aware that the user can change their decision by going to the application settings (TV Provider permission access) or to *`Settings -> TV Provider`* on iOS and iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.
   
  The streaming application can request the user's permission when the application enters the foreground state, because the application can check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information at any point before requiring user authentication.

>[!IMPORTANT]
>
> Assumptions
>
> <br/>
>
> * The streaming application has completed the [onboarding prerequisites](/help/authentication/single-sign-on/partner-single-sign-on/apple-single-sign-on/apple-sso-overview.md#apple-sso-prerequisites-programmer) that apply to a Programmer and are required to enable the Apple single sign-on user experience. 

### Workflow {#apple-sso-cookbook-rest-api-v2-workflow}

Perform the given steps to implement the Apple single sign-on using partner flows as shown in the following diagram.

![Apple single sign-on using partner flows](/help/authentication/assets/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-apple-single-sign-on-using-partner-flows.png)

*Apple single sign-on using partner flows*

+++A. Registration Phase

1. **Retrieve client credentials:** The streaming application gathers all the necessary data to retrieve client credentials by calling the Client Register endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve client credentials](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-client-credentials.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `software_statement`
   > * All the _required_ headers, like `Content-Type`, `X-Device-Info`
   > * All the _optional_ parameters and headers

1. **Return client credentials:** The Client Register endpoint response contains information about the client credentials associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve client credentials](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-client-credentials.md#success) API documentation for details on the information provided in a client credentials response.
   >
   > <br/>
   >
   > The Client Register validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Retrieve client credentials](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-client-credentials.md#error) API documentation.

   >[!TIP]
   >
   > Suggestion: The client credentials must be cached and may be used indefinitely.

1. **Retrieve access token:** The streaming application gathers all the necessary data to retrieve access token by calling the Client Token endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve access token](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `client_id`, `client_secret`, and `grant_type`
   > * All the _required_ headers, like `Content-Type`, `X-Device-Info`
   > * All the _optional_ parameters and headers

1. **Return access token:** The Client Token endpoint response contains information about the access token associated with the received parameters and headers.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve access token](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md#success) API documentation for details on the information provided in an access token response.
   >
   > <br/>
   >
   > The Client Token validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Retrieve access token](/help/authentication/dcr-api/apis/dynamic-client-registration-apis-retrieve-access-token.md#error) API documentation.

   >[!TIP]
   >
   > Suggestion: The access token must be cached and used only within the specified duration (e.g., 24-hour time-to-live). After it expires, the streaming application must request a new access token.

+++

+++B. Check Authentication Phase

1. **Retrieve partner framework status:** The streaming application calls the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) developed by Apple, to obtain user permission and provider information.

   >[!IMPORTANT]
   >
   > Refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) documentation for details on:
   >
   > <br/>
   >
   > * The streaming application must check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
   > * The streaming application must provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the `VSAccountManager`.
   > * The streaming application must submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
   > * The streaming application must wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.
   >
   > <br/>
   >
   > The streaming application must ensure it specifies a Boolean value equal to `false` for the [`isInterruptionAllowed`](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest/1771708-isinterruptionallowed) property in the `VSAccountMetadataRequest` object, to indicate that the user cannot be interrupted at this phase.

1. **Return partner framework status information:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Retrieve profiles:** The streaming application gathers all the necessary data to retrieve all profiles information by sending a request to the Profiles endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profiles](/help/authentication/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md#Request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`, and `AP-Partner-Framework-Status`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the partner framework status such that the retrieved response may include an "appleSSO" type profile.
   >
   > <br/>
   >
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Return information about found profiles:** The Profiles endpoint response contains information about the found profiles associated with the received parameters and headers.

1. **Choose a profile and proceed with decisions flows:** If the Profiles endpoint response contains profiles, the streaming application uses its internal logic (eventually by interacting with the end user) to choose one of the available profiles to continue with subsequent decisions flows.

1. **Proceed with partner authentication flow:** If the Profiles endpoint response does not contain a profile, the streaming application continues with partner authentication flow.

+++

+++C. Partner Authentication Phase

1. **Retrieve configuration:** The streaming application gathers all the necessary data to retrieve the list of MVPDs having an active integration by sending a request to the Configuration endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve configuration for specific service provider](/help/authentication/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md#Request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`, and `X-Device-Info`
   > * All the _optional_ parameters and headers

1. **Return configuration:** The Configuration endpoint response contains information about the MVPDs having an active integration with the service provider.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve configuration for specific service provider](/help/authentication/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md#Response) API documentation for details on the information provided in a configuration response.
   >
   > <br/>
   >
   > The Configuration endpoint validates the request data to ensure that basic conditions are met:
   >
   > * The _required_ parameters and headers must be valid.
   >
   > <br/>
   >
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md)

   >[!IMPORTANT]
   >
   > The streaming application must ensure it processes the following details provided for each MVPD when proceeding further:
   >
   > * `enablePlatformServices`: Indicates whether the MVPD currently supports the Apple single sign-on.
   > * `displayInPlatformPicker`: Indicates whether the MVPD can be displayed in the Apple picker.
   > * `boardingStatus`: Indicates whether the MVPD is onboarded in the Apple single sign-on.

1. **Retrieve partner framework status:** The streaming application calls the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) developed by Apple, to obtain user permission and provider information.

   >[!IMPORTANT]
   >
   > Refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) documentation for details on:
   >
   > <br/>
   >
   > * The streaming application must check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
   > * The streaming application must provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the `VSAccountManager`.
   > * The streaming application must submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
   > * The streaming application must wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.
   >
   > <br/>
   >
   > The streaming application must ensure it specifies a Boolean value equal to `true` for the [`isInterruptionAllowed`](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest/1771708-isinterruptionallowed) property in the `VSAccountMetadataRequest` object, to indicate that the user can be interrupted to select TV provider at this phase.

1. **Return partner framework status information:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Retrieve partner authentication request:** The streaming application gathers all the necessary data to initiate an authentication session by calling the Sessions Partner endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve partner authentication request](/help/authentication/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md#Request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider` and `partner`
   > * All the _required_ headers like `Authorization`, `AP-Device-Identifier`, `Content-Type`, `X-Device-Info`, and `AP-Partner-Framework-Status`
   > * All the _optional_ headers and parameters
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the partner framework status such that the retrieved response may include a partner authentication request (SAML request).
   >
   > <br/>
   >
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Indicate the next action:** The Sessions Partner endpoint response contains the necessary data to guide the streaming application regarding the next action.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve partner authentication request](/help/authentication/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md#Response) API documentation for details on the information provided in a session response.
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
   > If basic validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.
   >
   > <br/>
   >
   > The Sessions Partner endpoint validates the request data to ensure that partner single sign-on conditions are met:
   >
   >  * The partner single sign-on configuration in the Adobe Pass server must be valid and enabled.
   >  * The partner framework status payload received via the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) header must be valid.
   >
   > <br/>
   >
   > If partner single sign-on validation fails, the response will default to the basic authentication flow.

1. **Proceed with decisions flows:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to "authorize".
   * The `actionType` attribute is set to "direct".

   If the Adobe Pass backend identifies a valid profile, the streaming application does not need to re-authenticate with the selected MVPD, as there is already a profile that can be used for subsequent decisions flows.

1. **Proceed with basic authentication flow:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to either "authenticate" or "resume".
   * The `actionType` attribute is set to either "interactive" or "direct".

   If the Adobe Pass backend does not identify a valid profile and the partner single sign-on validation fails, the Adobe Pass server falls back to the basic authentication flow.

   For more details about the basic authentication flow, refer to the following documents:
   * [Perform authentication within primary application](/help/authentication/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
   * [Perform authentication within secondary application with preselected mvpd](/help/authentication/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
   * [Perform authentication within secondary application without preselected mvpd](/help/authentication/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)

1. **Proceed with retrieve profile using partner authentication response flow:** The Sessions Partner endpoint response contains the following data:
   * The `actionName` attribute is set to "partner_profile".
   * The `actionType` attribute is set to "direct".
   * The `authenticationRequest - type` attribute includes the security protocol used by the partner framework for MVPD login (currently set to SAML only).
   * The `authenticationRequest - request` attribute includes the SAML request that is passed to the partner framework.
   * The `authenticationRequest - attributesNames` attribute includes the SAML attributes that are passed to the partner framework.

   If the Adobe Pass backend does not identify a valid profile and the partner single sign-on validation passes, the streaming application receives a response with actions and data to pass to the partner framework for starting the authentication flow with the MVPD.

1. **Complete MVPD authentication with partner framework:** Forward the partner authentication request (SAML request) obtained in previous step to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount). If the authentication flow is successful, the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) interaction with the MVPD produces a partner authentication response (SAML response) that is returned along with the partner framework status information.

   >[!IMPORTANT]
   >
   > Refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) documentation for details on:
   >
   > <br/>
   >
   > * The streaming application must check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
   > * The streaming application must provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the `VSAccountManager`.
   > * The streaming application must submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information and must include the partner authentication request (SAML request) obtained in previous step.
   > * The streaming application must wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.
   >
   > <br/>
   >
   > The streaming application must ensure it specifies a Boolean value equal to `true` for the [`isInterruptionAllowed`](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest/1771708-isinterruptionallowed) property in the `VSAccountMetadataRequest` object, to indicate that the user can be interrupted to authenticate with the selected TV provider at this phase.

1. **Return partner authentication response:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.
   * The partner authentication response (SAML response) is present and valid.

1. **Retrieve profile using partner authentication response:** The streaming application gathers all the necessary data to create and retrieve a profile by calling the Profiles Partner endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile using partner authentication response](/help/authentication/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md#Request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `partner`, and `SAMLResponse`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`, `Content-Type`, `X-Device-Info`, and `AP-Partner-Framework-Status`
   > * All the _optional_ headers and parameters
   >
   > <br/>
   >
   > The streaming application must ensure it includes valid values for the partner framework status and the partner authentication response (SAML response) such that the retrieved response may include an "appleSSO" type profile.
   >
   > <br/>
   >
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.
   
1. **Return information about partner profile:** The Profiles endpoint response contains information about the partner profile, including the attribute `type` set to "appleSSO".

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve profile using partner authentication response](/help/authentication/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md#Response) API documentation for details on the information provided in a profile response.
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
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.
   >
   > <br/>
   >
   > The Profiles Partner endpoint validates the request data to ensure that partner single sign-on conditions are met:
   >
   >  * The partner single sign-on configuration in the Adobe Pass server must be valid and enabled.
   >  * The partner framework status payload received via the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) header must be valid.
   >
   > <br/>
   >
   > If partner single sign-on validation fails, the response will default to the basic profile retrieval flow.

1. **Proceed with decisions flows:** The streaming application can continue with subsequent decisions flows.

+++

+++ D. Decisions Phase

1. **Retrieve partner framework status:** The streaming application calls the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) developed by Apple, to obtain user permission and provider information.

   >[!IMPORTANT]
   >
   > Refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) documentation for details on:
   >
   > <br/>
   >
   > * The streaming application must check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
   > * The streaming application must provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the `VSAccountManager`.
   > * The streaming application must submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
   > * The streaming application must wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.
   >
   > <br/>
   >
   > The streaming application must ensure it specifies a Boolean value equal to `false` for the [`isInterruptionAllowed`](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest/1771708-isinterruptionallowed) property in the `VSAccountMetadataRequest` object, to indicate that the user cannot be interrupted at this phase.

   >[!TIP]
   > 
   > Suggestion: The streaming application can use a cached value for the partner framework status information, that we recommend refreshing when the application transitions from background to foreground state. 

1. **Return partner framework status information:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Retrieve preauthorization decisions:** The streaming application gathers all the necessary data to obtain preauthorization decisions for a list of resources by calling the Decisions Preauthorize endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve preauthorization decisions using specific mvpd](/help/authentication/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `resources`
   > * All the _required_ headers, like `Authorization` and `AP-Device-Identifier`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request further, when the chosen profile is an "appleSSO" type profile.
   >
   > <br/>
   >
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Return preauthorization decisions:** The Decisions Preauthorize endpoint response contains a `Permit` or `Deny` decision for each resource:
   * A `Permit` decision means the resource is playable. The response does not include a media token, as the preauthorization flow must not be used to play resources.
   * A `Deny` decision means the resource is not playable. The response includes an error payload which adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve preauthorization decisions using specific mvpd](/help/authentication/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md#response) API documentation for details on the information provided in a decision response.
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
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.

1. **Retrieve partner framework status:** The streaming application calls the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) developed by Apple, to obtain user permission and provider information.

   >[!IMPORTANT]
   >
   > Refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) documentation for details on:
   >
   > <br/>
   >
   > * The streaming application must check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
   > * The streaming application must provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the `VSAccountManager`.
   > * The streaming application must submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
   > * The streaming application must wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.
   >
   > <br/>
   >
   > The streaming application must ensure it specifies a Boolean value equal to `false` for the [`isInterruptionAllowed`](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest/1771708-isinterruptionallowed) property in the `VSAccountMetadataRequest` object, to indicate that the user cannot be interrupted at this phase.

   >[!TIP]
   >
   > Suggestion: The streaming application can use a cached value for the partner framework status information, that we recommend refreshing when the application transitions from background to foreground state.

1. **Return partner framework status information:** The streaming application validates the response data to ensure that basic conditions are met:
   * The user permission access status is granted.
   * The user provider mapping identifier is present and valid.
   * The user provider profile's expiration date (if available) is valid.

1. **Retrieve authorization decision:** The streaming application gathers all the necessary data to obtain an authorization decision for a specific resource by calling the Decisions Authorize endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authorization decisions using specific mvpd](/help/authentication/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `resources`
   > * All the _required_ headers, like `Authorization` and `AP-Device-Identifier`
   > * All the _optional_ parameters and headers
   >
   > <br/>
   >
   > The streaming application must ensure it includes a valid value for the partner framework status before making a request further, when the chosen profile is an "appleSSO" type profile.
   >
   > <br/>
   >
   > For more details about `AP-Partner-Framework-Status` header, refer to the [AP-Partner-Framework-Status](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md) documentation.

1. **Return authorization decision:** The Decisions Authorize endpoint response contains a `Permit` or `Deny` decision for the specific resource:
   * A `Permit` decision means the resource is playable. The response includes a media token.
   * A `Deny` decision means the resource is not playable. The response includes an error payload which adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.

   >[!IMPORTANT]
   >
   > Refer to the [Retrieve authorization decisions using specific mvpd](/help/authentication/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md#response) API documentation for details on the information provided in a decision response.
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
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.

+++

+++ D. Logout Phase

1. **Initiate Adobe Pass logout:** The streaming application gathers all the necessary data to initiate the logout flow by calling the Adobe Pass Logout endpoint.

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](/help/authentication/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md#request) API documentation for details on:
   >
   > * All the _required_ parameters, like `serviceProvider`, `mvpd`, and `redirectUrl`
   > * All the _required_ headers, like `Authorization`, `AP-Device-Identifier`
   > * All the _optional_ parameters and headers

1. **Indicate the next action:** The Adobe Pass Logout endpoint response contains the necessary data to guide the streaming application regarding the next action.

   >[!IMPORTANT]
   >
   > Refer to the [Initiate logout for specific mvpd](/help/authentication/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md#response) API documentation for details on the information provided in a logout response.
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
   > If validation fails, an error response will be generated, providing additional information that adheres to the [Enhanced Error Codes](/help/authentication/enhanced-error-codes.md) documentation.

   >[!IMPORTANT]
   > 
   > The streaming application must ensure it indicates the user to continue to log out from partner level further.

+++
