---
title: REST API V2 FAQs
description: REST API V2 FAQs
exl-id: 2dd74b47-126e-487b-b467-c16fa8cc14c1
---
# REST API V2 FAQs {#rest-api-v2-faqs}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This document provides high overview answers for frequently asked questions about the Adobe Pass Authentication REST API V2 adoption.

For more information about the REST API V2 overall, see the [REST API V2 Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md) documentation.

## General FAQs {#general-faqs}

Start with this section if you are working on an application that needs to integrate the REST API V2, whether it is a new application or an existing one that migrates from [REST API V1](#migration-rest-api-v1-to-rest-api-v2) or [SDK](#migration-sdk-to-rest-api-v2).

For more information about migration details and steps, see the next sections too.

### Registration Phase FAQs {#registration-phase-faqs-general}

+++Registration Phase FAQs

Refer to the [Dynamic Client Registration (DCR) FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md#rest-api-v2-access-faqs) documentation.

+++

### Configuration Phase FAQs {#configuration-phase-faqs-general}

+++Configuration Phase FAQs

#### 1. What's the purpose of the Configuration Phase? {#configuration-phase-faq1}

The purpose of the Configuration Phase is to provide the client application the list of MVPDs with which it is actively integrated along with configuration details (e.g., `id`, `displayName`, `logoUrl`, etc.) saved by Adobe Pass Authentication for each MVPD.

The Configuration Phase acts as a prerequisite step for the Authentication Phase when the client application needs to ask the user to select their TV Provider.

#### 2. Is the Configuration Phase mandatory? {#configuration-phase-faq2}

The Configuration Phase is not mandatory, the client application must retrieve the configuration only when the user needs to select their MVPD to authenticate or re-authenticate.

The client application can skip this phase in the following scenarios:

* The user is already authenticated.
* The user is offered temporary access through basic or promotional [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) feature.
* The user authentication has expired, but the client application has cached the previously selected MVPD as a user experience motivated choice, and just prompts the user to confirm that they are still a subscriber of that MVPD.

#### 3. What's a configuration and how long is it valid? {#configuration-phase-faq3}

The configuration is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#configuration) documentation.

The configuration contains a list of MVPDs defined by the following attributes `id`, `displayName`, `logoUrl`, etc., that can be retrieved from the [Configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) endpoint.

The client application must retrieve the configuration only when the user needs to select their MVPD to authenticate or re-authenticate.

The client application can use the configuration response to present a UI picker with available MVPD options whenever the user needs to select their TV provider.

The client application must store the user's selected MVPD identifier, as specified by the MVPD's configuration-level `id` attribute, to proceed with the Authentication, Preauthorization, Authorization, or Logout phases.

For more information, refer to the [Retrieve configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) documentation.

#### 4. Is the configuration specific to a service provider, platform, or user? {#configuration-phase-faq4}

The configuration is specific to a [service provider](rest-api-v2-glossary.md#service-provider).

The configuration is specific to a platform type.

The configuration is not specific to a user.

For client applications using a server-to-server architecture, it is recommended to cache the configuration response (e.g., with a 2-minute TTL) for each platform type in server-side memory storage. This reduces unnecessary requests for each user and improves overall user experience.

#### 5. Should the client application cache the configuration response information in a persistent storage? {#configuration-phase-faq5}

>[!IMPORTANT]
> 
> For client applications using a server-to-server architecture, it is recommended to cache the configuration response (e.g., with a 2-minute TTL) for each platform type in server-side memory storage. This reduces unnecessary requests for each user and improves overall user experience.

The client application must retrieve the configuration only when the user needs to select their MVPD to authenticate or re-authenticate.

The client application should cache the configuration response information in a memory storage to avoid unnecessary requests and improve the user experience when:

* The user is already authenticated.
* The user is offered temporary access through basic or promotional [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) feature.
* The user authentication has expired, but the client application has cached the previously selected MVPD as a user experience motivated choice, and just prompts the user to confirm that they are still a subscriber of that MVPD.

#### 6. Can the client application manage its own list of MVPDs? {#configuration-phase-faq6}

The client application can manage its own list of MVPDs, but it would require to keep the MVPD identifiers in sync with Adobe Pass Authentication. Therefore, it is recommended to use the configuration provided by Adobe Pass Authentication to ensure the list is up to date and accurate.

The client application would receive an [error](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) from Adobe Pass Authentication REST API V2 if the provided MVPD identifier is invalid or in case it does not have an active integration with the specified [service provider](rest-api-v2-glossary.md#service-provider).

#### 7. Can the client application filter the list of MVPDs? {#configuration-phase-faq7}

The client application can filter the list of MVPDs provided in the configuration response by implementing a custom mechanism based on its own business logic and requirements such as user location or user history of previous selection.

The client application can filter the list of [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) MVPDs or the MVPDs that have their integration still in development or testing.

#### 8. What happens if the integration with an MVPD is disabled and marked as inactive? {#configuration-phase-faq8}

When the integration with an MVPD is disabled and marked as inactive, then the MVPD is removed from the list of MVPDs provided in further configuration responses, and there are two important consequences to consider:

* The unauthenticated users of that MVPD will no longer be able to complete the Authentication Phase using that MVPD.
* The authenticated users of that MVPD will no longer be able to complete the Preauthorization, Authorization, or Logout Phases using that MVPD.

The client application would receive an [error](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) from Adobe Pass Authentication REST API V2 if the user selected MVPD does not have anymore an active integration with the specified [service provider](rest-api-v2-glossary.md#service-provider).

#### 9. What happens if the integration with an MVPD is enabled back and marked as active? {#configuration-phase-faq9}

When the integration with an MVPD is enabled back and marked as active, then the MVPD is included back in the list of MVPDs provided in further configuration responses, and there are two important consequences to consider:

* The unauthenticated users of that MVPD will be able again to complete the Authentication Phase using that MVPD.
* The authenticated users of that MVPD will be able again to complete the Preauthorization, Authorization, or Logout Phases using that MVPD.

#### 10. How to enable or disable the integration with an MVPD? {#configuration-phase-faq10}

This operation can be completed through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#disable-integration) documentation.

+++

### Authentication Phase FAQs {#authentication-phase-faqs-general}

+++Authentication Phase FAQs

#### 1. What's the purpose of the Authentication Phase? {#authentication-phase-faq1}

The purpose of the Authentication Phase is to provide the client application the capability to verify the user's identity and obtain user metadata information.

The Authentication Phase acts as a prerequisite step for the Preauthorization Phase or Authorization Phase when the client application needs to play content.

#### 2. Is the Authentication Phase mandatory? {#authentication-phase-faq2}

The Authentication Phase is mandatory, the client application must authenticate the user when it does not have a valid profile within Adobe Pass Authentication.

The client application can skip this phase in the following scenarios:

* The user is already authenticated and the profile is still valid.
* The user is offered temporary access through basic or promotional [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) feature.

The client application error handling requires to handle the [error](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) codes (e.g., `authenticated_profile_missing`, `authenticated_profile_expired`,  `authenticated_profile_invalidated`, etc.), which indicate that the client application requires the user to authenticate.

#### 3. What's an authentication session and how long is it valid? {#authentication-phase-faq3}

The authentication session is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#session) documentation.

The authentication session stores information about the initiated authentication process that can be retrieved from the Sessions endpoint.

The authentication session is valid for a limited and short timeframe specified at the moment of issue by the `notAfter` timestamp, indicating the amount of time the user has to complete the authentication process before requiring to restart the flow.

The client application can use the authentication session response to know how to proceed with the authentication process. Take notice that there are cases in which the user is not required to authenticate, such as providing temporary access, degraded access, or when the user is already authenticated.

For more information, refer to the following documents:

* [Create authentication session API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
* [Resume authentication session API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
* [Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
* [Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)

#### 4. What's an authentication code and how long is it valid? {#authentication-phase-faq4}

The authentication code is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#code) documentation.

The authentication code stores a unique value generated when a user initiates the authentication process, and uniquely identifies a user's authentication session until the process is complete or until the authentication session expires.

The authentication code is valid for a limited and short timeframe specified at the moment of initiating the authentication session by the `notAfter` timestamp, indicating the amount of time the user has to complete the authentication process before requiring to restart the flow.

The client application can use the authentication code to verify whether the user has successfully completed authentication and retrieve the user's profile information, typically through a polling mechanism.

The client application can also use the authentication code to allow the user to complete or resume the authentication process either on the same device or on a second (screen) one, considering that the authentication session did not expire.

For more information, refer to the following documents:

* [Create authentication session API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
* [Resume authentication session API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
* [Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
* [Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)

#### 5. How can the client application know if the user typed a valid authentication code and that the authentication session did not expire yet? {#authentication-phase-faq5}

The client application can validate the authentication code that is typed by the user in a secondary (screen) application by sending a request to one of the Sessions endpoint responsible to resume authentication session or retrieve authentication session information associated with the authentication code.

The client application would receive an [error](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) if the provided authentication code was typed wrong or in case the authentication session would be expired.

For more information, refer to the [Resume authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) and [Retrieve authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md) documents.

#### 6. How can the client application know if the user is already authenticated? {#authentication-phase-faq6}

The client application can query one of the following endpoints capable of verifying if a user is already authenticated and return profile information:

* [Profiles endpoint API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Profiles endpoint for specific MVPD API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Profiles endpoint for specific (authentication) code API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

For more details, refer to the following documents:

* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

#### 7. What's a profile and how long is it valid? {#authentication-phase-faq7}

The profile is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#profile) documentation.

The profile stores information about the user's authentication validity, metadata information and many more that can be retrieved from the Profiles endpoint.

The client application can use the profile to know the user's authentication status, access user metadata information, find the method used to authenticate or the entity used to provide identity.

For more details, refer to the following documents:

* [Profiles endpoint API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Profiles endpoint for specific MVPD API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Profiles endpoint for specific (authentication) code API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)
* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

The profile is valid for a limited timeframe specified when queried by the `notAfter` timestamp, indicating the amount of time the user has a valid authentication before requiring to go through the Authentication Phase again.

This limited timeframe known as authentication (authN) [TTL](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#ttl) can be viewed and changed through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#most-used-flows) documentation.

#### 8. Should the client application cache the user's profile information in a persistent storage? {#authentication-phase-faq8}

The client application should cache parts of the user's profile information in a persistent storage to avoid unnecessary requests and improve the user experience considering the following aspects:

| Attribute    | User Experience                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mvpd`       | The client application can use this to keep track of the user's selected TV provider and continue to use it further during Preauthorization or Authorization Phases.<br/><br/>When the current user profile expires, the client application can use the remembered MVPD selection and just ask the user to confirm.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `attributes` | The client application can use this to personalize the user experience based on different [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) keys (e.g., `zip`, `maxRating`, etc.).<br/><br/>User metadata becomes available after the authentication flow completes, therefore the client application does not need to query a separate endpoint to retrieve the [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) information, as it is already included in the profile information.<br/><br/>Certain metadata attributes may be updated during the authorization flow, depending on the MVPD and the specific metadata attribute. As a result, the client application may need to query the Profiles APIs again to retrieve the latest user metadata. |
| `notAfter`   | The client application can use this to keep track of user profile expiration date.<br/><br/>The client application error handling requires to handle the [error](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) codes (e.g., `authenticated_profile_missing`, `authenticated_profile_expired`,  `authenticated_profile_invalidated`, etc.), which indicates that the client application requires the user to authenticate.                                                                                                                                                                                                                                                                                                                                                            |

#### 9. Can the client application extend the user's profile without requiring re-authentication? {#authentication-phase-faq9}

No.

The user profile cannot be extended beyond its validity without user interaction, as its expiration is determined by the authentication TTL established with MVPDs.

Therefore, the client application must prompt the user to re-authenticate and interact with the MVPD login page to refresh their profile on our system.

However, for MVPDs that support [home-based authentication](/help/premium-workflow/hba-access/home-based-authentication.md) (HBA), the user will not be required to enter credentials.

#### 10. What are the use cases for each available Profiles endpoint? {#authentication-phase-faq10}

The basic Profiles endpoints are designed to provide client application the capability to know the user's authentication status, access user metadata information, find the method used to authenticate or the entity used to provide identity.

Each endpoint suits a specific use case, as follows:

| API                                                                                                                                                                                                                     | Description                                                               | Use case                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Profiles endpoint API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)                                                     | Retrieve all user profiles.                                               | **User opens the client application for the first time**<br/><br/>In this scenario, the client application does not have the user's selected MVPD identifier cached in persistent storage.<br/><br/>As a result, it will send a single request to retrieve all available user profiles.                                                           |
| [Profiles endpoint for specific MVPD API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)                  | Retrieve the user profile associated with a specific MVPD.                | **User returns to the client application after authenticating in a previous visit**<br/><br/>In this case, the client application must have the user's previously selected MVPD identifier cached in persistent storage.<br/><br/>As a result, it will send a single request to retrieve the user's profile for that specific MVPD.               |
| [Profiles endpoint for specific (authentication) code API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | Retrieve the user profile associated with a specific authentication code. | **User initiates the authentication process**<br/><br/>In this scenario, the client application must determine whether the user has successfully completed authentication and retrieve their profile information.<br/><br/>As a result, it will start a polling mechanism to retrieve the user's profile associated with the authentication code. |

For more details, refer to the [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md) and [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md) documents.

The Profiles SSO endpoint serves a different purpose, it provides the client application the capability to create a user profile using the partner authentication response and retrieve it in a single, one-time operation.

| API                                                                                                                                                                                                                                      | Description                                                             | Use case                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Profiles SSO endpoint API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md) | Create and retrieve user profile using partner authentication response. | **User permits the application to use partner single-sign-on to authenticate**<br/><br/>In this scenario, the client application must create a user profile after receiving the partner authentication response and retrieve it in a single, one-time operation. |

For any subsequent queries, the basic Profiles endpoints must be used to determine the user's authentication status, access user metadata information, find the method used to authenticate or the entity used to provide identity. 

For more details, refer to the [Single sign-on using partner flows](/help/premium-workflow/sso-access/partner-sso/apple-sso/apple-sso-cookbook-rest-api-v2.md) documents.

#### 11. What should the client application do if the user has multiple MVPD profiles? {#authentication-phase-faq11}

The decision to support multiple profiles depends on the client application’s business requirements.

Most users will have only one profile. However, in cases where multiple profiles exist (as detailed below), the client application is responsible for determining the best user experience for profile selection.

The client application may choose to prompt the user to select the desired MVPD profile or make the selection automatically, such as choosing the first user profile from the response or the one with the longest validity period.

REST API v2 supports multiple profiles to accommodate:

* Users who may have to choose between a regular MVPD profile and one obtained via single sign-on (SSO).
* Users being offered temporary access without requiring to log out from their regular MVPD.
* Users with MVPD subscription combined with Direct-to-Consumer (DTC) services.
* Users with multiple MVPD subscriptions.

#### 12. What happens when user profiles expire? {#authentication-phase-faq12}

When user profiles expire, they are no longer included in the response from the Profiles endpoint.

If the Profiles endpoint returns an empty profiles map response, the client application must create a new authentication session and prompt the user to re-authenticate.

For more information, refer to the [Create authentication session API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) documentation.

#### 13. When do user profiles become invalid? {#authentication-phase-faq13}

User profiles become invalid in the following scenarios:

* When the authentication TTL expires, as indicated by the `notAfter` timestamp in the Profiles endpoint response.
* When the client application changes the [AP-Device-Identifier](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md) header value.
* When the client application updates the client credentials used to retrieve the [Authorization](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md) header value.
* When the client application revokes or updates the software statement used to obtain client credentials.

#### 14. When should the client application start the polling mechanism? {#authentication-phase-faq14}

To ensure efficiency and avoid unnecessary requests, the client application must start the polling mechanism under the following conditions:

**Authentication performed within the primary (screen) application**

The primary (streaming) application should start polling when the user reaches the final destination page, after the browser component loads the URL specified for the `redirectUrl` parameter in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint request.

**Authentication performed within a secondary (screen) application**

The primary (streaming) application should start polling as soon as the user initiates the authentication process—right after receiving the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response and displaying the authentication code to the user.

#### 15. When should the client application stop the polling mechanism? {#authentication-phase-faq15}

To ensure efficiency and avoid unnecessary requests, the client application must stop the polling mechanism under the following conditions:

**Successful authentication** 

The user's profile information is successfully retrieved, confirming their authentication status. At this point, polling is no longer needed.

**Authentication session and code expiry**

The authentication session and code expire, as indicated by the `notAfter` timestamp (e.g., 30 minutes) in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response. If this happens, the user must restart the authentication process, and polling using the previous authentication code should be stopped immediately.

**New authentication code generated** 

If the user requests a new authentication code on the primary (screen) device, the existing session is no longer valid, and polling using the previous authentication code should be stopped immediately.

#### 16. What interval between calls should the client application use for the polling mechanism? {#authentication-phase-faq16}

To ensure efficiency and avoid unnecessary requests, the client application must configure the polling mechanism frequency under the following conditions:

| **Authentication performed within the primary (screen) application**       | **Authentication performed within a secondary (screen) application**       |
|----------------------------------------------------------------------------|----------------------------------------------------------------------------|
| The primary (streaming) application should poll every 3-5 seconds or more. | The primary (streaming) application should poll every 3-5 seconds or more. |

#### 17. What's the maximum number of polling requests the client application can send? {#authentication-phase-faq17}

The client application must adhere to the current limits defined by the Adobe Pass Authentication [Throttling Mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md#throttling-mechanism-limits).

The client application error handling must be able to handle the [429 Too Many Requests](/help/authentication/integration-guide-programmers/throttling-mechanism.md#throttling-mechanism-response) error code, which indicates that the client application has exceeded the maximum number of requests allowed.

For more details, refer to the [Throttling Mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

#### 18. How can the client application get the user's metadata information? {#authentication-phase-faq18}

The client application can query one of the following endpoints capable to return [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) information as part of the profile information:

* [Profiles endpoint API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Profiles endpoint for specific MVPD API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Profiles endpoint for specific (authentication) code API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

User metadata becomes available after the authentication flow completes, therefore the client application does not need to query a separate endpoint to retrieve the [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) information, as it is already included in the profile information.

For more details, refer to the following documents:

* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

Certain metadata attributes may be updated during the authorization flow, depending on the MVPD and the specific metadata attribute. As a result, the client application may need to query the above APIs again to retrieve the latest user metadata.

#### 19. How should the client application manage degraded access? {#authentication-phase-faq19}

The [Degradation Feature](/help/premium-workflow/degraded-access/degradation-feature.md) enables the client application to maintain a seamless streaming experience for users, even when their MVPD's authentication or authorization services encounter issues.

As a summary, this can ensure uninterrupted access to content despite MVPD temporary service disruptions.

Given that your organization intends to use the premium degradation feature, the client application must handle degraded access flows, which outline how REST API v2 endpoints behave in such scenarios.

For more details, refer to the [Degraded access flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/degraded-access-flows/rest-api-v2-access-degraded-flows.md) documentation.

#### 20. How should the client application manage temporary access? {#authentication-phase-faq20}

The [TempPass Feature](/help/premium-workflow/temporary-access/temp-pass-feature.md) enables the client application to provide temporary access to the user.

As a summary, this can engage users by providing time-limited access to content or a predefined number of VOD titles for a specified time period.

Given that your organization intends to use the premium TempPass feature, the client application must handle temporary access flows, which outline how REST API v2 endpoints behave in such scenarios.

In previous API versions, the client application had to log out a user authenticated with their regular MVPD to offer temporary access.

With REST API v2, the client application can seamlessly switch between a regular MVPD and a TempPass MVPD when authorizing a stream, eliminating the need for the user to be logged out.

For more details, refer to the [Temporary access flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md) documentation.

#### 21. How should the client application manage cross-device single sign-on access? {#authentication-phase-faq21}

REST API v2 can enable cross-device single sign-on if the client application provides a consistent unique user identifier across devices.

This identifier, known as a service token, must be generated by the client application through the implementation or integration of an external Identity Service of choice.

For more details, refer to the [Single sign-on using service token flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md) documentation.

+++

### Preauthorization Phase FAQs {#preauthorization-phase-faqs-general}

+++Preauthorization Phase FAQs

#### 1. What's the purpose of the Preauthorization Phase? {#preauthorization-phase-faq1}

The purpose of the Preauthorization Phase is to provide the client application the capability to present a subset of resources from its catalog that the user would be entitled to access.

The Preauthorization Phase can enhance the user experience when the user opens the client application for the first time or navigates to a new section.

#### 2. Is the Preauthorization Phase mandatory? {#preauthorization-phase-faq2}

The Preauthorization Phase is not mandatory, the client application can skip this phase if it wants to present a catalog of resources without filtering them first based on the user's entitlement.

#### 3. What's a preauthorization decision? {#preauthorization-phase-faq3}

The preauthorization is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#preauthorization) documentation, while the decision term can also be found in the [Glossary](rest-api-v2-glossary.md#decision).

The preauthorization decision stores information about the MVPD preauthorization process enquiry result that can be retrieved from the Decisions Preauthorize endpoint.

The client application can use the preauthorization decisions to present a subset of resources the TV Provider (informative) decisions would allow the user to access.

For more details, refer to the following documents:

* [Retrieve preauthorization decisions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)
* [Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)

#### 4. Should the client application cache the preauthorization decisions in a persistent storage? {#preauthorization-phase-faq4}

The client application is not required to store preauthorization decisions in persistent storage. However, it is recommended to cache permit decisions in memory to improve the user experience. This helps avoid unnecessary calls to the Decisions Preauthorize endpoint for resources that have already been preauthorized, reducing latency and improving performance.

#### 5. How can the client application determine why a preauthorization decision was denied? {#preauthorization-phase-faq5}

The client application can determine the reason for a denied preauthorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Preauthorize endpoint. These details provide insight into the specific reason the preauthorization request was denied, helping to inform the user experience or trigger any necessary handling in the application.

Ensure that any retry mechanism implemented for retrieving preauthorization decisions does not result in an endless loop if the preauthorization decision is denied.

Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

#### 6. Why is the preauthorization decision missing a media token? {#preauthorization-phase-faq6}

The preauthorization decision is missing a media token because the Preauthorization Phase must not be used to play resources, as that is the purpose of the Authorization Phase.

#### 7. Can the Authorization Phase be skipped if a preauthorization decision already exists? {#preauthorization-phase-faq7}

No.

The Authorization Phase cannot be skipped even if a preauthorization decision is available. Preauthorization decisions are informational only and do not grant actual playback rights. The Preauthorization Phase is intended to provide early guidance, but the Authorization Phase is still required before playing any content.

#### 8. What is a resource and what formats are supported? {#preauthorization-phase-faq8}

The resource is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#resource) documentation.

The resource is a unique identifier that is agreed upon with MVPDs and is associated with a content that the client application could stream.

The resource unique identifier can have two formats:

* A simple string format such as a unique identifier for a channel (brand).
* A media RSS (MRSS) format containing additional information such as the title, ratings and parental-control metadata.

For more details, refer to the [Protected Resources](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md#protected-resources) documentation.

#### 9. For how many resources can the client application obtain a preauthorization decision at a time? {#preauthorization-phase-faq9}

The client application can obtain a preauthorization decision for a limited number of resources in a single API request, usually up to 5, due to conditions imposed by MVPDs.

This maximum number of resources can be viewed and changed after agreeing with MVPDs through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#add-more-properties) documentation.

+++

### Authorization Phase FAQs {#authorization-phase-faqs-general}

+++Authorization Phase FAQs

#### 1. What's the purpose of the Authorization Phase? {#authorization-phase-faq1}

The purpose of the Authorization Phase is to provide the client application the capability to play resources the user requests after validating their rights with the MVPD.

#### 2. Is the Authorization Phase mandatory? {#authorization-phase-faq2}

The Authorization Phase is mandatory, the client application cannot skip this phase if it wants to play resources the user requests, as it requires verifying with the MVPD that the user is entitled before releasing the stream.

#### 3. What's an authorization decision and how long is it valid? {#authorization-phase-faq3}

The authorization is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#authorization) documentation, while the decision term can also be found in the [Glossary](rest-api-v2-glossary.md#decision).

The authorization decision stores information about the MVPD authorization process enquiry result that can be retrieved from the Decisions Authorize endpoint.

The client application can use the authorization decision containing a media token to play the resource stream in case the TV Provider (authoritative) decision would allow the user to access it.

For more details, refer to the following documents:

* [Retrieve authorization decisions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)
* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)

The authorization decision is valid for a limited and short timeframe specified at the moment of issue, indicating the amount of time it will be cached by Adobe Pass Authentication before requiring to query the MVPD again.

This limited timeframe known as authorization (authZ) [TTL](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#ttl) can be viewed and changed through the Adobe Pass [TVE Dashboard](rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#most-used-flows) documentation.

#### 4. Should the client application cache the authorization decisions in a persistent storage? {#authorization-phase-faq4}

The client application is not required to store authorization decisions in persistent storage.

#### 5. How can the client application determine why an authorization decision was denied? {#authorization-phase-faq5}

The client application can determine the reason for a denied authorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Authorize endpoint. These details provide insight into the specific reason the authorization request was denied, helping to inform the user experience or trigger any necessary handling in the application.

Ensure that any retry mechanism implemented for retrieving authorization decisions does not result in an endless loop if the authorization decision is denied.

Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

#### 6. What's a media token and how long is it valid? {#authorization-phase-faq6}

The media token is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#media-token) documentation.

The media token consists of a signed string sent in clear text that can be retrieved from the Decisions Authorize endpoint.

For more information, refer to the [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier) documentation.

The media token is valid for a limited and short timeframe specified at the moment of issue, indicating the time limit before it must be verified and used by the client application.

The client application can use the media token to play a resource stream in case the TV Provider (authoritative) decision would allow the user to access it.

For more details, refer to the following documents:

* [Retrieve authorization decisions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)
* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)

#### 7. Should the client application validate the media token before playing the resource stream? {#authorization-phase-faq7}

Yes.

The client application must validate the media token before starting playback of the resource stream. This validation should be performed using the [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier). By verifying the `serializedToken` from the returned `token`, the client application helps prevent unauthorized access, such as stream ripping, and ensures that only properly authorized users can play the content.

#### 8. Should the client application refresh an expired media token during playback? {#authorization-phase-faq8}

No.

The client application is not required to refresh an expired media token while the stream is actively playing. If the media token expires during playback, the stream should be allowed to continue uninterrupted. However, the client must request a new authorization decision — and obtain a new media token — the next time the user attempts to play a resource.

#### 9. What is the purpose of each timestamp attribute in the authorization decision? {#authorization-phase-faq9}

The authorization decision includes several timestamp attributes that provide essential context about the validity period of the authorization itself and the associated media token. These timestamps serve different purposes, depending on whether they relate to the authorization decision or the media token.

**Decision-Level Timestamps**

These timestamps describe the validity period of the overall authorization decision:

| Attribute   | Description                                                          | Notes                                                                                                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `notBefore` | The time in milliseconds when the authorization decision was issued. | This marks the start of the authorization validity window.                                                                                                                                                                                                                                                   |
| `notAfter`  | The time in milliseconds when the authorization decision expires.    | The [authorization Time-to-Live (TTL)](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md#authorization-ttl-management) determines how long the authorization remains valid before requiring re-authorization. This TTL is negotiated with MVPD representatives. |

**Token-Level Timestamps**

These timestamps describe the validity period of the media token that is tied to the authorization decision:

| Attribute   | Description                                               | Notes                                                                                                                                                                                                          |
|-------------|-----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `notBefore` | The time in milliseconds when the media token was issued. | This marks when the token becomes valid for playback.                                                                                                                                                          |
| `notAfter`  | The time in milliseconds when the media token expires.    | Media tokens have a deliberately short lifespan (typically 7 minutes) to minimize misuse risks and account for potential clock differences between the token-generating server and the token-verifying server. |

#### 10. What is a resource and what formats are supported? {#authorization-phase-faq10}

The resource is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#resource) documentation.

The resource is a unique identifier that is agreed upon with MVPDs and is associated with a content that the client application could stream.

The resource unique identifier can have two formats:

* A simple string format such as a unique identifier for a channel (brand).
* A media RSS (MRSS) format containing additional information such as the title, ratings and parental-control metadata.

For more details, refer to the [Protected Resources](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md#protected-resources) documentation.

#### 11. For how many resources can the client application obtain an authorization decision at a time? {#authorization-phase-faq11}

The client application can obtain an authorization decision for a limited number of resources in a single API request, usually up to 1, due to conditions imposed by MVPDs.

+++

### Logout Phase FAQs {#logout-phase-faqs-general}

+++Logout Phase FAQs

#### 1. What's the purpose of the Logout Phase? {#logout-phase-faq1}

The purpose of the Logout Phase is to provide the client application the capability to terminate the user's authenticated profile within Adobe Pass Authentication upon user request.

#### 2. Is the Logout Phase mandatory? {#logout-phase-faq2}

The Logout Phase is mandatory, the client application must provide the user with the capability to log out.

+++

### Headers FAQs {#headers-faqs-general}

+++Headers FAQs

#### 1. How to compute the value for the Authorization header? {#headers-faq1}

>[!IMPORTANT]
>
> In case the client application is migrating from REST API V1 to REST API V2, the client application can continue to use the same method to obtain the `Bearer` access token value as before.

The [Authorization](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md) request header contains the `Bearer` access token required by the client application to access Adobe Pass protected APIs.

The Authorization header value must be obtained from Adobe Pass Authentication during the Registration Phase.

For more details, refer to the following documents:

* [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)
* [Retrieve client credentials API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
* [Retrieve access token API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)
* [Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)

#### 2. How to compute the value for the AP-Device-Identifier header? {#headers-faq2}

>[!IMPORTANT]
>
> In case the client application is migrating from REST API V1 to REST API V2, the client application can continue to use the same method to compute the device identifier value as before.

The [AP-Device-Identifier](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md) request header contains the streaming device identifier as it was created by the client application.

The [AP-Device-Identifier](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md) header documentation provides examples for major platforms of how to compute the value, but the client application can choose to use a different method based on its own business logic and requirements.

#### 3. How to compute the value for the X-Device-Info header? {#headers-faq3}

>[!IMPORTANT]
>
> In case the client application is migrating from REST API V1 to REST API V2, the client application can continue to use the same method to compute the device information value as before.

The [X-Device-Info](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) request header contains the client information (device, connection and application) related to the actual streaming device and is used to determine platform-specific rules that MVPDs may enforce.

The [X-Device-Info](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) header documentation provides examples for major platforms of how to compute the value, but the client application can choose to use a different method based on its own business logic and requirements.

If the [X-Device-Info](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) header is missing or contains incorrect values, the request may be classified as originating from an `unknown` platform. 

This can lead to the request being treated as insecure, and subject to more restrictive rules, such as shorter authentication TTLs. Additionally, some fields, such as the streaming device `connectionIp` and `connectionPort`, are mandatory for features like Spectrum's [Home Base Authentication](/help/premium-workflow/hba-access/home-based-authentication.md).

Even when the request originates from a server on behalf of a device, the [X-Device-Info](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) header value must reflect the actual streaming device information.

+++

### Misc FAQs {#misc-faqs-general}

+++Misc FAQs

#### 1. Can I explore REST API V2 requests and responses and test the API? {#misc-faq1}

Yes.

You can explore REST API V2 through our dedicated [Adobe Developer](https://developer.adobe.com/adobe-pass/) website. The Adobe Developer website provides unrestricted access to:

* [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/)
* [REST API V2](https://developer.adobe.com/adobe-pass/api/rest_api_v2/interactive/)

To interact with [REST API V2](https://developer.adobe.com/adobe-pass/api/rest_api_v2/interactive/), you must include the [Authorization](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md) header with a `Bearer` access token obtained via the [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/).

For using the [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/), a software statement with REST API V2 scope is required. For more details, refer to the [Dynamic Client Registration (DCR) FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md) document.

#### 2. Can I explore REST API V2 requests and responses using an API development tool with OpenAPI support? {#misc-faq2}

Yes.

You can download OpenAPI specification files for the [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/) and [REST API V2](https://developer.adobe.com/adobe-pass/api/rest_api_v2/interactive/) from the [Adobe Developer](https://developer.adobe.com/adobe-pass/) website.

To download the OpenAPI specification files, click the download buttons to save the following files to your local machine:

* [DCR API JSON](https://developer.adobe.com/adobe-pass/dcrApi.json)
* [REST API V2 JSON](https://developer.adobe.com/adobe-pass/restApiV2.json)

You can then import these files into your preferred API development tool to explore REST API V2 requests and responses and test the API.

#### 3. Can I still use the existing API test tool hosted at https://sp.auth-staging.adobe.com/apitest/api.html? {#misc-faq3}

No.

The client applications migrating to REST API V2 should use the new test tool hosted at https://developer.adobe.com/adobe-pass/. The Adobe Developer website provides unrestricted access to:

* [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/)
* [REST API V2](https://developer.adobe.com/adobe-pass/api/rest_api_v2/interactive/)

To interact with [REST API V2](https://developer.adobe.com/adobe-pass/api/rest_api_v2/interactive/), you must include the [Authorization](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md) header with a `Bearer` access token obtained via the [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/).

For using the [DCR API](https://developer.adobe.com/adobe-pass/api/dcr_api/interactive/), a software statement with REST API V2 scope is required. For more details, refer to the [Dynamic Client Registration (DCR) FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md) document.

+++

## Migration FAQs {#migration-faqs}

Continue with this section if you are working on an application that needs to migrate an existing application to REST API V2.

>[!MORELIKETHIS]
>
> * [Dynamic Client Registration (DCR) FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md#migration-faqs)

### General Migration FAQs {#general-migration-faqs}

+++General Migration FAQs

#### 1. Am I required to roll out a new client application migrated to REST API V2 to all users at once? {#migration-faq1}

No.

The client application is not required to roll out a new version integrating the REST API V2 to all users simultaneously.

Adobe Pass Authentication will continue to support older client application versions integrating the REST API V1 or SDK through the end of 2025.

#### 2. Am I required to roll out a new client application migrated to REST API V2 across all APIs and flows at once? {#migration-faq2}

Yes.

The client application is required to roll out a new version integrating the REST API V2 across all Adobe Pass Authentication APIs and flows simultaneously.

In case of the 'second screen authentication' flow, the client application is required to roll out a new version integrating the REST API V2 for both the [primary](rest-api-v2-glossary.md#primary-application) and [secondary](rest-api-v2-glossary.md#secondary-application) applications simultaneously.

Adobe Pass Authentication will not support 'hybrid' implementations that integrate both REST API V2 and REST API V1/SDK between APIs and flows.

#### 3. Will the user authentication be preserved when updating to a new client application migrated to REST API V2? {#migration-faq3}

No.

The user authentication obtained within older client application versions integrating the REST API V1 or SDK will not be preserved.

Therefore, the user will be required to re-authenticate within the new client application migrated to REST API V2.

#### 4. Are the enhanced error codes enabled by default in REST API V2? {#migration-faq4}

Yes.

The client applications migrating to REST API V2 automatically benefit from this feature by default, providing more detailed and precise error information.

For more details, refer to the [Enhanced Error Codes](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2) documentation.

#### 5. Do existing integrations require configuration changes when migrating to REST API V2? {#migration-faq5}

No.

The client applications migrating to REST API V2 do not require any configuration changes for existing MVPD integrations. Also, they will continue to use the same identifiers for existing [service providers](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#service-provider) and [MVPDs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#mvpd).

Additionally, the protocols used by Adobe Pass Authentication to communicate with MVPD endpoints remain unchanged.

+++

### Migration from REST API V1 to REST API V2 {#migration-rest-api-v1-to-rest-api-v2-faqs}

Continue with this subsection if you are working on an application that needs to migrate from REST API V1 to REST API V2.

#### Registration Phase FAQs {#registration-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Registration Phase FAQs

##### 1. What are the high-level API migrations required for the Registration Phase? {#registration-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are no high level changes in regard to the Registration Phase.

The client application can continue to use the same flow to register against Adobe Pass Authentication through the [Dynamic Client Registration (DCR)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#dcr) process and obtain an access token.

For more information, refer to the following documents:

* [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)
* [Retrieve client credentials API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
* [Retrieve access token API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)
* [Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)

+++

#### Configuration Phase FAQs {#configuration-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Configuration Phase FAQs

##### 1. What are the high-level API migrations required for the Configuration Phase? {#configuration-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are high level changes to consider that are presented in the following table:

| Scope                                          | REST API V1                                                                                                                                   | REST API V2                                                                                                                                                                                                                                  | Observations | 
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Retrieve list of MVPDs with active integration | [GET <br/> /api/v1/config/{serviceProvider}](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/provide-mvpd-list.md) | [GET <br/> /api/v2/{serviceProvider}/configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) |              |

+++

#### Authentication Phase FAQs {#authentication-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Authentication Phase FAQs

##### 1. What are the high-level API migrations required for the Authentication Phase? {#authentication-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are high level changes to consider that are presented in the following table:

| Scope                                                       | REST API V1                                                                                                                                                                                                                                                                                                                                    | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve registration code (authentication code)            | [POST <br/> /reggie/v1/{serviceProvider}/regcode](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md)                                                                                                                                                                                     | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check registration code (authentication code)               | [GET <br/> /reggie/v1/{serviceProvider}/regcode/{code}](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/return-registration-record.md)                                                                                                                                                                              | [GET <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Resume (MVPD) authentication on second screen (application) | [GET <br/> /api/v1/authenticate](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)                                                                                                                                                                                                        | [POST <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                          | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Initiate (MVPD) authentication                              | [GET <br/> /api/v1/authenticate](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)                                                                                                                                                                                                        | [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                               | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status                            | [GET <br/> /api/v1/checkauthn (first screen)](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md) <br/> [GET <br/> /api/v1/checkauthn (second screen)](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-flow-by-second-screen-web-app.md) | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user authentication token (profile)                | [GET <br/> /api/v1/tokens/authn](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md)                                                                                                                                                                                                  | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information                          | [GET <br/> /api/v1/tokens/usermetadata](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md)                                                                                                                                                                                                           | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

+++

#### Preauthorization Phase FAQs {#preauthorization-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Preauthorization Phase FAQs

##### 1. What are the high-level API migrations required for the Preauthorization Phase? {#preauthorization-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are high level changes to consider that are presented in the following table:

| Scope                                                         | REST API V1                                                                                                                                                                                                                                                                                                                                                                     | REST API V2                                                                                                                                                                                                                                              | Observations                                                                                                                                                                                                                                                                                                     | 
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve preauthorized resources (preauthorization decisions) | [GET <br/> /api/v1/preauthorize (first screen)](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-list-of-preauthorized-resources.md) <br/> [GET <br/> /api/v1/preauthorize (second screen)](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | [POST <br/> /api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)</li></ul> |

+++

#### Authorization Phase FAQs {#authorization-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Authorization Phase FAQs

##### 1. What are the high-level API migrations required for the Authorization Phase? {#authorization-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are high level changes to consider that are presented in the following table:

| Scope                                                 | REST API V1                                                                                                                                  | REST API V2                                                                                                                                                                                                                                        | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate (MVPD) authorization                         | [GET <br/> /api/v1/authorize](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authorization.md)          | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |
| Retrieve authorization token (authorization decision) | [GET <br/> /api/v1/tokens/authz](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authorization-token.md) | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |                                                                                                                                            
| Retrieve short authorization token (media token)      | [GET <br/> /api/v1/tokens/media](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/obtain-short-media-token.md)     | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |

+++

#### Logout Phase FAQs {#logout-phase-faqs-migration-rest-api-v1-to-rest-api-v2}

+++Logout Phase FAQs

##### 1. What are the high-level API migrations required for the Logout Phase? {#logout-phase-v1-to-v2-faq1}

In the migration from REST API V1 to REST API V2 there are high level changes to consider that are presented in the following table:

| Scope           | REST API V1                                                                                                               | REST API V2                                                                                                                                                                                          | Observations                                                                                                                                                                                                                                                                                 | 
|-----------------|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate logout | [GET <br/> /api/v1/logout](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-logout.md) | [GET <br/> /api/v2/{serviceProvider}/logout](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)</li></ul> |

+++

### Migration from SDK to REST API V2 {#migration-sdk-to-rest-api-v2}

Continue with this subsection if you are working on an application that needs to migrate from SDK to REST API V2.

#### Registration Phase FAQs {#registration-phase-faqs-migration-sdk-to-rest-api-v2}

+++Registration Phase FAQs

##### 1. What are the high-level API migrations required for the Registration Phase? {#registration-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope                                      | SDK                                         | REST API V2                                                                                                                                                                                                                                                                                                                                                 | Observations                                                                                                                                                                                                                                                                                                                                                                                          | 
|--------------------------------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Complete Dynamic Client Registration (DCR) | Providing software statement to constructor | [POST <br/> /o/client/register](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)</li><li>[Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)</li></ul> |

###### AccessEnabler iOS/tvOS SDK

| Scope                                      | SDK                                         | REST API V2                                                                                                                                                                                                                                                                                                                                                 | Observations                                                                                                                                                                                                                                                                                                                                                                                          | 
|--------------------------------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Complete Dynamic Client Registration (DCR) | Providing software statement to constructor | [POST <br/> /o/client/register](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)</li><li>[Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)</li></ul> |

###### AccessEnabler Android SDK

| Scope                                      | SDK                                         | REST API V2                                                                                                                                                                                                                                                                                                                                                 | Observations                                                                                                                                                                                                                                                                                                                                                                                          | 
|--------------------------------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Complete Dynamic Client Registration (DCR) | Providing software statement to constructor | [POST <br/> /o/client/register](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)</li><li>[Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)</li></ul> |

###### AccessEnabler FireOS SDK

| Scope                                      | SDK                                         | REST API V2                                                                                                                                                                                                                                                                                                                                                 | Observations                                                                                                                                                                                                                                                                                                                                                                                          | 
|--------------------------------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Complete Dynamic Client Registration (DCR) | Providing software statement to constructor | [POST <br/> /o/client/register](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)</li><li>[Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)</li></ul> |

+++

#### Configuration Phase FAQs {#configuration-phase-faqs-migration-sdk-to-rest-api-v2}

+++Configuration Phase FAQs

##### 1. What are the high-level API migrations required for the Configuration Phase? {#configuration-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope                                          | SDK                                                                                                                                                       | REST API V2                                                                                                                                                                                                                                  | Observations | 
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Retrieve list of MVPDs with active integration | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#getAuthN) | [GET <br/> /api/v2/{serviceProvider}/configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) |              |

###### AccessEnabler iOS/tvOS SDK

| Scope                                          | SDK                                                                                                                                                  | REST API V2                                                                                                                                                                                                                                  | Observations | 
|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Retrieve list of MVPDs with active integration | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN) | [GET <br/> /api/v2/{serviceProvider}/configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) |              |

###### AccessEnabler Android SDK

| Scope                                          | SDK                                                                                                                                                 | REST API V2                                                                                                                                                                                                                                  | Observations | 
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Retrieve list of MVPDs with active integration | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#getAuthN) | [GET <br/> /api/v2/{serviceProvider}/configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) |              |

###### AccessEnabler FireOS SDK

| Scope                                          | SDK                                                                                                                                                                | REST API V2                                                                                                                                                                                                                                  | Observations | 
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Retrieve list of MVPDs with active integration | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#getAuthN) | [GET <br/> /api/v2/{serviceProvider}/configuration](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) |              |

+++

#### Authentication Phase FAQs {#authentication-phase-faqs-migration-sdk-to-rest-api-v2}

+++Authentication Phase FAQs

##### 1. What are the high-level API migrations required for the Authentication Phase? {#authentication-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope                              | SDK                                                                                                                                                                                                                                                                                                                           | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate (MVPD) authentication     | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#setSelProv) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status   | [AccessEnabler.checkAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#checkAuthN)                                                                                                                                                                 | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information | [AccessEnabler.getMetadata](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#getMeta)                                                                                                                                                                            | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

###### AccessEnabler iOS SDK

| Scope                              | SDK                                                                                                                                                                                                                                                                                                                 | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate (MVPD) authentication     | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setSelProv) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status   | [AccessEnabler.checkAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#checkAuthN)                                                                                                                                                            | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information | [AccessEnabler.getMetadata](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getMeta)                                                                                                                                                                       | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

###### AccessEnabler tvOS SDK

| Scope                                                       | SDK                                                                                                                                                                                                                                                                                                                 | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve registration code (authentication code)            | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setSelProv) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check registration code (authentication code)               | [GET <br/> /reggie/v1/{serviceProvider}/regcode/{code}](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/return-registration-record.md)                                                                                                                                                   | [GET <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Resume (MVPD) authentication on second screen (application) | [GET <br/> /api/v1/authenticate](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)                                                                                                                                                                             | [POST <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                          | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Initiate (MVPD) authentication                              | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setSelProv) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status                            | [AccessEnabler.checkAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#checkAuthN)                                                                                                                                                            | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information                          | [AccessEnabler.getMetadata](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getMeta)                                                                                                                                                                       | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

###### AccessEnabler Android SDK

| Scope                              | SDK                                                                                                                                                                                                                                                                                                                        | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate (MVPD) authentication     | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#setSelectedProvider) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status   | [AccessEnabler.checkAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#checkAuthN)                                                                                                                                                                    | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information | [AccessEnabler.getMetadata](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#getMetadata)                                                                                                                                                                           | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

###### AccessEnabler FireOS SDK

| Scope                                                       | SDK                                                                                                                                                                                                                                                                                                                                                      | REST API V2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve registration code (authentication code)            | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#setSelectedProvider) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check registration code (authentication code)               | [GET <br/> /reggie/v1/{serviceProvider}/regcode/{code}](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/return-registration-record.md)                                                                                                                                                                                        | [GET <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Resume (MVPD) authentication on second screen (application) | [GET <br/> /api/v1/authenticate](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)                                                                                                                                                                                                                  | [POST <br/> /api/v2/{serviceProvider}/sessions/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                          | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Initiate (MVPD) authentication                              | [AccessEnabler.getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#getAuthN) <br/> [AccessEnabler.setSelectedProvider](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#setSelectedProvider) | [POST <br/> /api/v2/{serviceProvider}/sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) <br/> [GET <br/> /api/v2/authenticate/{serviceProvider}/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)                                                                                                                                                                                                                                                 | For more details, refer to the following documents: <br/> <ul><li>[Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)</li><li>[Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)</li></ul>                                                                                                                                                                                                          |
| Check user authentication status                            | [AccessEnabler.checkAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#checkAuthN)                                                                                                                                                                                   | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |
| Retrieve user metadata information                          | [AccessEnabler.getMetadata](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#getMetadata)                                                                                                                                                                                          | Use one of the following: <br/><br/> [GET <br/> /api/v2/{serviceProvider}/profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md) <br/> [GET <br/> /api/v2/{serviceProvider}/profiles/code/{code}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) | The client application can use the response of these APIs for multiple purposes at once: <br/> <ul><li>Check user authentication status</li><li>Retrieve user profile</li><li>Retrieve user metadata information</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)</li><li>[Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)</li></ul> |

+++

#### Preauthorization Phase FAQs {#preauthorization-phase-faqs-migration-sdk-to-rest-api-v2}

+++Preauthorization Phase FAQs

##### 1. What are the high-level API migrations required for the Preauthorization Phase? {#preauthorization-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope                                                         | SDK                                                                                                                                                                                                                                                                                                                             | REST API V2                                                                                                                                                                                                                                              | Observations                                                                                                                                                                                                                                                                                                     | 
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve preauthorized resources (preauthorization decisions) | [AccessEnabler.checkPreauthorizedResources](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#checkPreauthRes) <br/> [AccessEnabler.preauthorize](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/preauthorize-api-javascript-sdk.md) | [POST <br/> /api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)</li></ul> |

###### AccessEnabler iOS/tvOS SDK

| Scope                                                         | SDK                                                                                                                                                                                                                                                                                                                 | REST API V2                                                                                                                                                                                                                                              | Observations                                                                                                                                                                                                                                                                                                     | 
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve preauthorized resources (preauthorization decisions) | [AccessEnabler.checkPreauthorizedResources](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#checkPreauth) <br/> [AccessEnabler.preauthorize](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/preauthorize-api-ios-tvos-sdk.md) | [POST <br/> /api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)</li></ul> |

###### AccessEnabler Android SDK

| Scope                                                         | SDK                                                                                                                                                                                                                                                                                                              | REST API V2                                                                                                                                                                                                                                              | Observations                                                                                                                                                                                                                                                                                                     | 
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve preauthorized resources (preauthorization decisions) | [AccessEnabler.checkPreauthorizedResources](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#checkPreauth) <br/> [AccessEnabler.preauthorize](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/preauthorize-api-android-sdk.md) | [POST <br/> /api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)</li></ul> |

| Scope                                                         | SDK                                                                                                                                                                              | REST API V2                                                                                                                                                                                                                                              | Observations                                                                                                                                                                                                                                                                                                     | 
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve preauthorized resources (preauthorization decisions) | [AccessEnabler.checkPreauthorizedResources](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#checkPreauth) | [POST <br/> /api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)</li></ul> |

+++

#### Authorization Phase FAQs {#authorization-phase-faqs-migration-sdk-to-rest-api-v2}

+++Authorization Phase FAQs

##### 1. What are the high-level API migrations required for the Authorization Phase? {#authorization-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope                                            | SDK                                                                                                                                                                                                                                                                                                                         | REST API V2                                                                                                                                                                                                                                        | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve short authorization token (media token) | [AccessEnabler.checkAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#checkAuthZ) <br/> [AccessEnabler.getAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#getAuthZ) | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler iOS/tvOS SDK

| Scope                                            | SDK                                                                                                                                                                                                                                                                                                               | REST API V2                                                                                                                                                                                                                                        | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve short authorization token (media token) | [AccessEnabler.checkAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#checkAuthZ) <br/> [AccessEnabler.getAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthZ) | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler Android SDK

| Scope                                            | SDK                                                                                                                                                                                                                                                                                                             | REST API V2                                                                                                                                                                                                                                        | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve short authorization token (media token) | [AccessEnabler.checkAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#checkAuthZ) <br/> [AccessEnabler.getAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#getAuthZ) | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler FireOS SDK

| Scope                                            | SDK                                                                                                                                                                                                                                                                                                                                           | REST API V2                                                                                                                                                                                                                                        | Observations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Retrieve short authorization token (media token) | [AccessEnabler.checkAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#checkAuthZ) <br/> [AccessEnabler.getAuthorization](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#getAuthZ) | [POST <br/> /api/v2/{serviceProvider}/decisions/authorize/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) | The client application can use the response of this API for multiple purposes at once: <br/> <ul><li>Initiate (MVPD) authorization</li><li>Retrieve authorization decision</li><li>Retrieve short media token</li></ul> <br/> For more details, refer to the following documents: <br/> <ul><li>[Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)</li></ul> |                                                                                                                                            

+++

#### Logout Phase FAQs {#logout-phase-faqs-migration-sdk-to-rest-api-v2}

+++Logout Phase FAQs

##### 1. What are the high-level API migrations required for the Logout Phase? {#logout-phase-sdk-to-v2-faq1}

In the migration from SDKs to REST API V2 there are high level changes to consider that are presented in the following tables:

###### AccessEnabler JavaScript SDK

| Scope           | SDK                                                                                                                                          | REST API V2                                                                                                                                                                                          | Observations                                                                                                                                                                                                                                                                                 | 
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate logout | [AccessEnabler.logout](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#logout) | [GET <br/> /api/v2/{serviceProvider}/logout](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler iOS/tvOS SDK

| Scope           | SDK                                                                                                                                     | REST API V2                                                                                                                                                                                          | Observations                                                                                                                                                                                                                                                                                 | 
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate logout | [AccessEnabler.logout](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#logout) | [GET <br/> /api/v2/{serviceProvider}/logout](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler Android SDK

| Scope           | SDK                                                                                                                                    | REST API V2                                                                                                                                                                                          | Observations                                                                                                                                                                                                                                                                                 | 
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate logout | [AccessEnabler.logout](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#logout) | [GET <br/> /api/v2/{serviceProvider}/logout](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)</li></ul> |                                                                                                                                            

###### AccessEnabler FireOS SDK

| Scope           | SDK                                                                                                                                                   | REST API V2                                                                                                                                                                                          | Observations                                                                                                                                                                                                                                                                                 | 
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initiate logout | [AccessEnabler.logout](/help/authentication/integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md#logout) | [GET <br/> /api/v2/{serviceProvider}/logout](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) | For more details, refer to the following documents: <br/> <ul><li>[Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)</li></ul> |                                                                                                                                            

+++
