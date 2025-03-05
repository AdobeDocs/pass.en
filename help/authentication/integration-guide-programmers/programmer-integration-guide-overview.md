---
title: Programmer integration guide
description: Programmer integration guide
exl-id: 51461caf-08ef-459e-b284-8f317f45e7b1
---
# Programmer integration guide {#programmer-integration-guide}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This integration guide is intended for content providers (Programmers) who plan to integrate with Adobe&reg; Pass Authentication.

In today’s digital landscape, viewers can access the Internet anytime, anywhere, and request access to your protected content. They might be looking to watch a one-time event or seeking the rights to stream an entire television series you are airing.

Before granting access to protected content, you must determine whether the viewer is entitled to it. Key questions include:

* **Does the viewer have an active subscription with a Multichannel Video Programming Distributor (MVPD)?**
* **Does that subscription include your programming?**

## Adobe Pass Authentication for TV Everywhere {#adobe-pass-authentication-for-tv-everywhere}

For Programmers, determining entitlement is not always straightforward. MVPDs are the custodians of their customers’ identifying data and access privileges. Complicating matters further, Programmers viewers may subscribe to a wide variety of MVPDs, each operating with unique systems. These complexities make verifying entitlement both technically challenging and resource-intensive.

![User Entitlement Determined Directly By Programmer](../assets/user-ent-by-progr.png){align="center"}

*User Entitlement Determined Directly By Programmer*

Adobe Pass Authentication securely facilitates entitlement transactions between Programmers and MVPDs, making it quick, easy, and secure to provide protected content to eligible viewers.

![User Entitlement Mediated by Adobe Pass Authentication](../assets/user-ent-mediatedby-authn.png){align="center"}

*User Entitlement Mediated by Adobe Pass Authentication*

Adobe Pass Authentication acts as a proxy and facilitates the entitlement flow between Programmers and MVPDs by offering secure and consistent interfaces for both parties.

For Programmers, Adobe Pass Authentication provides APIs as part of a **Standard** or a **Premium** tier:

* Standard Adobe Pass Authentication APIs:
    * [REST API DCR](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)
    * [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/rest-api-v2-apis-overview.md)

* Premium Adobe Pass Authentication APIs:
    * [Reset Temp Pass API](/help/authentication/integration-guide-programmers/features-premium/temporary-access/temp-pass-feature.md#reset-tempass-api-access)
    * [Degradation API](/help/authentication/integration-guide-programmers/features-premium/degraded-access/degradation-feature.md#degradation-api-access)
    * [Entitlement Service Monitoring API](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-api.md)

### Use Cases {#use-cases}

This section outlines further the Programmer integration use cases supported by Adobe Pass Authentication:

* Programmer (TVE) application with a single channel network

  This enables the Programmer to provide viewers with access to the content from a single-branded channel network within a TVE application.

* Programmer (TVE) application with multiple channel networks

  This enables the Programmer to provide viewers with access to the content from multiple channel networks within a single TVE application.

* Programmer (TVE) application for special events

  This enables the Programmer to provide viewers with access to the content of special events that may not be resources that are in the MVPD entitlement database like normal channels.

| **Phase**            | **Priority** | **Use Case**                                                            | **Documents**                                                                                                                                                                    |
|----------------------|--------------|-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Authentication**   | **High**     | Authentication                                                          | For more details, refer to the documents aggregated under the [Authentication Phase](#authentication-phase) section.                                                             |
|                      | **High**     | Home-Based Authentication (HBA)                                         | For more details, refer to the [Home-Based Authentication](/help/authentication/integration-guide-programmers/features-standard/hba-access/home-based-authentication.md).        |
|                      | **High**     | Single Sign-On (SSO)                                                    | For more details, refer to the documents aggregated under the [Single Sign-On (SSO)](#sso) section.                                                                              |
|                      | **High**     | Select MVPD                                                             | For more details, refer to the documents aggregated under the [Configuration Phase](#configuration-phase) section.                                                               |
|                      | **Medium**   | Branded MVPD Login Page                                                 | Enables MVPDs to provide login pages with branding specific to the Programmer or service provider, including support for default language preferences.                           |
|                      | **High**     | Configure Time-To-Live (TTL) Values Per Platform                        | For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#most-used-flows).             |
| **Preauthorization** | **Low**      | Preauthorization (Preflight Authorization)                              | For more details, refer to the documents aggregated under the [Preauthorization Phase](#preauthorization-phase) section.                                                         |
|                      | **Medium**   | Enhanced Error Codes                                                    | For more details, refer to the [Enhanced Error Codes](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md).             |
| **Authorization**    | **High**     | Authorization                                                           | For more details, refer to the documents aggregated under the [Authorization Phase](#authorization-phase) section.                                                               |
|                      | **High**     | Distinct Channel Authorization                                          | Enables users to access content from multiple channel networks within a single TVE application. Programmers can make channel-specific authorization calls to verify entitlement. |
|                      | **Low**      | Asset-Level Authorization                                               | Enables MVPDs to collect detailed analytics for individual content assets during authorization.                                                                                  |
|                      | **Medium**   | Enhanced Error Codes                                                    | For more details, refer to the [Enhanced Error Codes](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md).             |
|                      | **High**     | Programmer Federated Player - With Page-Level Authorization             | For more details, refer to the [Media Tokens](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md).                                |
|                      | **Medium**   | Programmer Federated Player - With Internal Player Authorization        | For more details, refer to the [Media Tokens](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md).                                |
|                      | **High**     | Syndicated Player - Hosted on MVPD Portal with Page-Level Authorization | For more details, refer to the [Media Tokens](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md).                                |
|                      | **Low**      | Parental Control - Content Ratings in Authorization Requests            | Enables the Programmer to include content ratings as part of the authorization request to the MVPD that are useful for asset-level authorization.                                |
|                      | **Low**      | Parental Control - Content Filtering Based on User Attributes           | Enables the Programmer to check the maximum content rating allowed for a user and filter the available content accordingly.                                                      |
| **Logout**           | **Medium**   | Logout                                                                  | For more details, refer to the documents aggregated under the [Logout Phase](#logout-phase) section.                                                                             |

## Entitlement Flow {#entitlement-flow}

The entitlement flow is a series of steps that a Programmer (TVE) application must complete to stream protected content. The flow consists of the following phases:

* [Registration Phase](#registration-phase)
* [Configuration Phase](#configuration-phase)
* [Authentication Phase](#authentication-phase)
* [(Optional) Preauthorization Phase](#preauthorization-phase)
* [Authorization Phase](#authorization-phase)
* [Logout Phase](#logout-phase)

On a user's initial visit to a Programmer (TVE) application, the entitlement flow follows the outlined sequence. However, on subsequent visits, the application may bypass certain steps based on the status of the registration or authentication and the applicable viewing policies.

For a detailed exploration of the entitlement flow and its phases, continue reading this document, and after refer to the accompanying cookbook guides for additional insights:

* [REST API V2 Cookbook (Client-to-Server)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/cookbooks/rest-api-v2-cookbook-client-server.md)
* [REST API V2 Cookbook (Server-to-Server)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/cookbooks/rest-api-v2-cookbook-server-server.md)

>[!NOTE]
>
> Programmer (TVE) application is used in this document to refer collectively to the types of applications running on different platforms (browsers, mobile devices, TV connected devices, etc.) supported by Adobe Pass Authentication.

### Registration Phase {#registration-phase}

The purpose of the Registration Phase is to register the client application against Adobe Pass Authentication through the [Dynamic Client Registration (DCR)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) process.

The Dynamic Client Registration (DCR) process requires the client application to obtain a pair of client credentials and retrieve an access token as the end goal of the Registration Phase.

**APIs**

* [Retrieve client credentials](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
* [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)

**Flows**

* [Dynamic client registration flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)

**FAQs**

* [Registration phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#registration-phase-faqs-general).

### Configuration Phase {#configuration-phase}

The purpose of the Configuration Phase is to provide the client application the list of MVPDs with which it is actively integrated along with configuration details saved by Adobe Pass Authentication for each MVPD.

The Configuration Phase acts as a prerequisite step for the Authentication Phase when the client application needs to ask the user to select their TV Provider.

**APIs**

* [Retrieve configuration for specific service provider](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md)

**FAQs**

* [Configuration phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#configuration-phase-faqs-general).

>[!TIP]
>
> The TVE application should include an MVPD selection interface, enabling users to easily identify and select their TV provider.

### Authentication Phase {#authentication-phase}

The purpose of the Authentication Phase is to provide the client application the capability to verify the user's identity with the MVPD and obtain user metadata information.

The Authentication Phase acts as a prerequisite step for the Preauthorization Phase or Authorization Phase when the client application needs to play content.

Successful authentication generates a profile tied to the application, device and service provider, containing also user metadata information.

**High-level Steps**

The following steps outline the high-level steps in case of a SAML integration:

1. **Programmer's Application (Website) Load**  
   The user navigates to the Programmer's application (website), which integrates Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md).

1. **Protected Content Request**  
   When the user attempts to access protected content, the Programmer's application displays a list of MVPDs for the user to select from.

1. **Authentication Request Initialization**  
   Upon MVPD selection, the user is redirected to an Adobe Pass Authentication server. Here, an encrypted SAML authentication request for the selected MVPD is generated, in case of a SAML integration. This request is sent on behalf of the Programmer to the MVPD. Depending on the MVPD's system, the user's browser is either redirected to the MVPD's login page or a login iFrame is embedded within the Programmer's application.

1. **MVPD Login**  
   The MVPD accepts the request and presents its login interface, either via redirect or iFrame.

1. **User Login and Validation**  
   The user logs in with their MVPD credentials. The MVPD validates the user's subscription status and establishes its own HTTP session.

1. **MVPD Response to Adobe Pass Authentication**  
   Once validation is complete, the MVPD generates a SAML response (encrypted) and sends it back to Adobe Pass Authentication.

1. **Profile Generation**  
   Adobe Pass Authentication verifies the SAML response, generates a user profile that gets cached, and redirects the user back to the Programmer's application (website).

**APIs**

* [Create authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
* [Resume authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
* [Retrieve authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)
* [Perform authentication in user agent](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)
* [Retrieve profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Retrieve profile for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Retrieve profile for specific code](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

**Flows**

* [Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
* [Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

**FAQs**

* [Authentication phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general).

>[!TIP]
>
> The TVE application should convey the user's authentication status clearly, for example, by displaying their MVPD logo alongside "locked" or "unlocked" icons to indicate the accessibility of protected content.

#### Single Sign-On (SSO) {#single-sign-on}

**APIs**

* [Retrieve partner authentication request](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md)
* [Create and retrieve profile using partner authentication response](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md)

**Flows**

* [Single sign-on using partner flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-partner-flows.md)
* [Single sign-on using platform identity flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md)
* [Single sign-on using service token flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md)

### (Optional) Preauthorization Phase {#preauthorization-phase}

The purpose of the Preauthorization Phase is to provide the client application the capability to present a subset of resources from its catalog that the user would be entitled to access.

The Preauthorization Phase can enhance the user experience when the user opens the client application for the first time or navigates to a new section.

**APIs**

* [Retrieve preauthorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)

**Flows**

* [Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)

**FAQs**

* [Preauthorization phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#preauthorization-phase-faqs-general).

>[!TIP]
>
> The TVE application should clearly differentiate restricted content from authorized content by using visual indicators, such as a "locked" icon for restricted content and an "unlocked" icon for authorized content.

### Authorization Phase {#authorization-phase}

The purpose of the Authorization Phase is to provide the client application the capability to play resources the user requests after validating their rights with the MVPD.

Successful authorization generates a decision, containing also a media token that is provided to the Programmer (TVE) application for security purposes.

**High-level Steps**

The following steps outline the high-level steps:

1. **Resource Identifier Handling**  
   The protected content is identified by a [resource identifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md#resource-identifier), which may be a simple string or a more complex structure. This identifier is predefined and agreed upon by the Programmer and the MVPD. The Programmer's application sends the resource identifier to the Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md).

1. **MVPD Authorization Check**  
   Adobe Pass Authentication server communicates with the MVPD's authorization endpoint using standardized protocols.

1. **MVPD Response to Adobe Pass Authentication**  
   Once validation is complete, the MVPD confirms the user is entitled (or not) to access the content and sends a response back to Adobe Pass Authentication.

1. **Decision and Media Token Generation**  
   Adobe Pass Authentication verifies the response, generates a [decision](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md) that gets cached, and returns the decision containing a media token back to the Programmer's application (website).

1. **Content Access Verification**  
   The Programmer's application uses the [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier) to confirm that the correct user is accessing the correct content. Once validated, the user is granted access to view the protected content.

**APIs**

* [Retrieve authorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)

**Flows**

* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)

**FAQs**

* [Authorization phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authorization-phase-faqs-general).

>[!TIP]
>
> The TVE application should clearly differentiate restricted content from authorized content by using visual indicators, such as a "locked" icon for restricted content and an "unlocked" icon for authorized content.

### Logout Phase {#logout-phase}

The purpose of the Logout Phase is to provide the client application the capability to terminate the user's authenticated profile within Adobe Pass Authentication upon user request.

**APIs**

* [Initiate logout for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md)

**Flows**

* [Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)

**FAQs**

* [Logout phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#logout-phase-faqs-general).

#### Single Logout (SLO) {#single-logout}

**Flows**

* [Single logout flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-logout-flow.md)

## Understanding Entitlements {#understanding-entitlements}

The Adobe Pass Authentication solution revolves around the creation of entitlements—specific pieces of data generated upon the successful completion of authentication and authorization workflows. These entitlements grant access to protected content but have a limited lifespan. Once an entitlement expires, it must be renewed by re-initiating the authentication or authorization processes.

For more details about entitlements, refer to the following documents:

* **Profiles**

  Upon successful authentication, Adobe Pass Authentication creates an authenticated profile ("long-lived") associated with the requesting application, device and service provider identifier (requestor identifier).

* **[User Metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md)**

  Upon successful authentication (and in some cases after authorization too), Adobe Pass Authentication receives user metadata from the MVPD that can expose it to the requesting application.

* **[Decisions](/help/authentication/integration-guide-programmers/features-standard/entitlements/decisions.md)**

  Upon successful authorization, Adobe Pass Authentication creates an authorization decision ("long-lived") associated with the requesting application, device, service provider identifier (requestor identifier) and a specific protected resource (resource identifier).

* **[Media Tokens](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md)**

  Upon successful authorization, Adobe Pass Authentication creates a media token ("short-lived") that is associated with a successful play request.
