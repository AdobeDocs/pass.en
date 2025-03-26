---
title: MVPD integration guide
description: MVPD integration guide
exl-id: b918550b-96a8-4e80-af28-0a2f63a02396
---
# MVPD integration guide {#mvpd-integration-guide}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This integration guide is intended for Multi-channel Video Programming Distributors (MVPDs) who plan to integrate with Adobe&reg; Pass Authentication.

TV Everywhere (TVE) is a transformative initiative in the Pay TV industry, enabling subscribers to access the content they already pay for across multiple devices, whether at home or on the go. For Pay TV providers, TVE offers significant opportunities among which strengthening existing customer relationships and opening doors to new ones. However, these opportunities come with challenges.

In the TVE ecosystem, **Programmers** supply the content, while **MVPDs** (Multichannel Video Programming Distributors) manage the customer data needed to verify if viewers are eligible subscribers. While coordinating authentication and authorization with a single Programmer may be manageable, doing so with dozens or even hundreds of Programmers introduces considerable complexity.

This is where **Adobe® Pass Authentication** simplifies the process. MVPDs only need to implement a single, streamlined integration with Adobe Pass to gain access to the entire TVE ecosystem. The provided integration framework speeds up time-to-market, provides a secure environment to mitigate fraud, and enhances the customer experience by delivering more TV content across multiple platforms.

## Adobe Pass Authentication for TV Everywhere {#adobe-pass-authentication-for-tv-everywhere}

Adobe Pass Authentication operates as a SaaS (Software as a Service) solution designed to enable rapid backend (server-to-server) integration, adhering to the business rules of both Multichannel Video Programming Distributors (MVPDs) and Programmers. 

### Standards and protocols {#standards-protocols}

Adobe Pass Authentication is fully aligned with the emerging standards and protocols for TV Everywhere (TVE), supporting seamless integration and compliance across the ecosystem.

* **CableLabs OLCA (Online Content Access) Specification**  
  Adobe Pass Authentication adheres to the CableLabs OLCA specification, which defines the technical requirements and architecture for delivering video content from online sources to Pay TV customers. Adobe actively participated in the CableLabs interoperability testing project in June 2011, successfully passing the testing process for a Service Provider implementation.

Adobe Pass Authentication is architected to support multiple protocols (e.g., SAML, OAuth 2.0, etc.), this flexibility allowing for future expansions, including custom protocols, based on evolving needs.

Most integrations use the SAML (Security Assertion Markup Language) protocol, a primary standard for authentication. Adobe Pass Authentication acts as a proxy Service Provider within the SAML framework, persisting the SAML authentication response as a secure token in the Adobe common domain.

Bottom line, Adobe Pass Authentication is protocol-agnostic, designed to align closely with OLCA standards. These standards establish a common framework for Programmers, MVPDs, and Service Providers, ensuring a cohesive approach to implementing TVE features.

### Integration and support {#integration-support}

Adobe Pass Authentication collaborates with MVPD technical teams to configure integrations tailored to their specific requirements, as follows:

* **Standard Integrations**  
  Offered free of charge, including documentation and basic email support.

* **Enhanced Support**  
  For significant customizations or expedited timelines, a support fee may apply.

Adobe Pass Authentication supports the efficient handling of MVPD business logic, as follows:

* **Self-Contained Business Logic**  
  For business logic enforced entirely by the MVPD during authorization requests, Adobe provides the necessary data. This data can include, but is not limited to, the unique device ID and the IP address for the user's device making the request.

* **Custom Property Support**  
  For business logic requiring user intervention or Adobe-specific handling, Adobe can maintain custom configurations for each MVPD. These policies enable pre-defined workflows that can be triggered at specific points in the entitlement workflow. For details, contact your Adobe representative.

## Entitlement Flow {#entitlement-flow}

The entitlement flow is a series of steps that a Programmer (TVE) application must complete to stream protected content. The flow includes several phases that involve interactions with the MVPD:

* [Authentication Phase](#authentication-phase)
* (Optional) Preauthorization Phase
* [Authorization Phase](#authorization-phase)
* Logout Phase

On a user's initial visit to a Programmer (TVE) application, the entitlement flow follows the outlined sequence. However, on subsequent visits, the application may bypass certain steps based on the status of the authentication and the applicable viewing policies.

>[!NOTE]
>
> Programmer (TVE) application is used in this document to refer collectively to the types of applications running on different platforms (browsers, mobile devices, TV connected devices, etc.) supported by Adobe Pass Authentication.

### Authentication Phase {#authentication-phase}

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

### Authorization Phase {#authorization-phase}

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

  Upon successful authorization, Adobe Pass Authentication creates a media token ("short-lived") that is associated with a successful play request and provides support for industry best practices for mitigating fraud (e.g., stream ripping).

The time-to-live ("TTL") values for profiles and decisions are set based on agreements between Programmers and Pay TV providers, who agree on a value that best serves everyone involved.
