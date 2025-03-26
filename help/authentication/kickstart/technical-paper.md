---
title: About Adobe Pass Authentication
description: About Adobe Pass Authentication
exl-id: 5edeaccb-f9fa-4395-83b4-706c518d5a03
---
# About Adobe&reg; Pass Authentication {#about-adobe-pass-authentication}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## About TV Everywhere {#about-tv-everywhere}

Today’s television viewers expect seamless access to Pay TV content anytime, anywhere. With the rise of Internet-connected devices, audiences are consuming content across an expanding range of platforms, including:

* Laptops
* Tablets
* Smartphones
* Websites
* Federated Apps
* Game Consoles
* Set-top Boxes
* Smart TVs

TV Everywhere is an industry initiative that ensures Pay TV subscribers can access the content they already pay for across multiple devices, both inside and outside their homes.

While traditional (linear) TV remains strong, the fastest-growing segments of video consumption are time-shifted content, online streaming, and alternative screens. This shift has disrupted the video distribution market, making TV Everywhere a crucial solution that aligns the interests of **Programmers, Pay TV providers, and subscribers.**

### Goals of TV Everywhere {#goals-tv-everywhere}

**Technical Goal**

* Enable Pay TV customers to access their subscribed content seamlessly across all devices and platforms.

**Business Goals**

* Preserve and strengthen existing customer relationships while enabling new opportunities.
* Empower Programmers and content owners to reach broader audiences and maximize the value of premium content.
* Extend brands through direct online engagement with viewers.

### Challenges of TV Everywhere {#challenges-tv-everywhere}

With the opportunities of TV Everywhere come significant challenges, entitlement being the most critical. Before a viewer can access subscription content, a system must verify their entitlement.

Key questions include:

* Does the user have an active subscription with a Pay TV provider?
* Does their subscription include the requested content?

Determining entitlement is particularly challenging for Programmers and content owners because Pay TV operators control customer data and access privileges.

Beyond entitlement, several technical and integration challenges arise, including:

* Developing a multi-device strategy that ensures seamless access.
* Managing complex relationships between Programmers and Pay TV providers.
* Preventing fraudulent access and enforcing terms of service.
* Delivering a consistent, user-friendly authentication experience across websites and apps.
* Maintaining fast time-to-market to align with affiliate agreements.
* Controlling costs associated with multiple integrations.

These challenges make direct integrations between Programmers and multiple Pay TV authentication systems highly resource-intensive, requiring both time and technical expertise.

To overcome these hurdles, **Adobe® Pass Authentication** simplifies and streamlines entitlement verification, enabling seamless, secure access to TV Everywhere content.

## Introduction to Adobe Pass Authentication {#introduction-adobe-pass-authentication}

Adobe Pass Authentication securely mediates entitlement transactions between Programmers and Pay TV providers, ensuring that the right customers can access the right content effortlessly.

![](../assets/programmers-connect-authn.png)

*Some of the Programmers and Pay TV providers who connect through Adobe Pass Authentication*

**Who benefits from Adobe Pass Authentication**

* **Programmers** 

  Who want to easily integrate with Pay TV providers, also known as MVPDs (Multichannel Video Programming Distributors), to reach the widest audience and optimize revenue.

* **Pay TV providers (MVPDs)**

  Who seek to connect with multiple content owners (Programmers) through a single integration, enhancing customer satisfaction by facilitating access to subscription content online.

* **Pay TV customers**

  Who want to watch the content they already pay for anytime, anywhere, on any device. 

**Programmers**

Programmers looking to maximize audience reach and revenue can:

* Integrate easily with top Pay TV providers without managing multiple direct connections.
* Expand their audience by ensuring authentication across all major providers and platforms.
* Protect premium content with secure authentication, restricting access to authorized users and devices.
* Enable Single Sign-On (SSO) to improve the user experience across apps and websites.

**Pay TV providers (MVPDs)**

Pay TV providers can enhance customer experience and streamline operations by:

* Connecting with multiple content owners through a single integration.
* Offering a branded, seamless viewing experience across devices and platforms.
* Ensuring secure authentication to prevent unauthorized access and manage concurrent streams per household.

**Pay TV customers**

Subscribers benefit from TV Everywhere, allowing them to watch the content they already pay for anytime, anywhere, on any device.

### Integrating with Adobe Pass Authentication {#integrating-adobe-pass-authentication}

Whether you are a Pay TV provider or a Programmer, integrating with Adobe Pass Authentication requires active participation. Below is a high overview of the process for both roles.

#### Programmer Integration Process {#programmer-integration-process}

Additional guidance is available once the integration is formally initiated, but the process typically involves the following steps:

**Prerequisites**

* A content management system (CMS).
* A content delivery mechanism, which may include a third-party content delivery network (CDN).
* An existing online video platform with a media player either embedded in a website or a standalone application.

**Integration Tasks**

* Integrate the Adobe Pass Authentication [REST API DCR](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md).
* Integrate the Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/rest-api-v2-apis-overview.md).
* Integrate the Adobe Pass Authentication [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier).
* Develop a user interface for the authentication, authorization and logout workflow.

For more details on the Programmer integration process, refer to the [Programmer kickstart guide](/help/authentication/kickstart/programmer-kickstart-guide.md) and [Programmer integration guide](/help/authentication/integration-guide-programmers/programmer-integration-guide-overview.md) documents.

#### Pay TV Provider Integration Process {#pay-tv-provider-integration-process}

Additional guidance is available once the integration is formally initiated, but the process typically involves the following steps:

**Prerequisites**

* Sign the Adobe Pass Authentication Non-Disclosure Agreement (NDA).
* Provide the Adobe Pass Authentication engineering team with specifications for the authentication and authorization system. A SAML-based identity provider (IdP) for authentication and a SOAP-based authorization system are recommended for the simplest integration.

**Integration Tasks**

* Establish connectivity with Adobe Pass Authentication servers.
* Complete Staging Release and ensure quality assurance.
* Complete Production Release and ensure quality assurance.

Standard integration is free of charge for Pay TV providers, including documentation and basic email support. However, providers requiring extensive assistance or accelerated timelines may incur a support fee or choose to work with an experienced third-party partner, such as Synacor.

Adobe Pass Authentication can efficiently support Pay TV provider-specific business logic in two key ways:

* For business logic that is self-contained and applied by the Pay TV provider when an authorization request is received, Adobe provides the necessary data (e.g., unique device ID, IP address) to support enforcement.
* For business logic that requires user intervention or specific handling by Adobe, custom properties can be maintained for each Pay TV provider. These configurations may include pre-defined workflows triggered at specific points in the authentication process.

For more details on the Pay TV provider integration process, refer to the [MVPD kickstart guide](/help/authentication/kickstart/mvpd-kickstart-guide.md) and [MVPD integration guide](/help/authentication/integration-guide-mvpds/mvpd-integration-guide-overview.md) documents.

### Entitlement Flow {#entitlement-flow}

Adobe Pass Authentication acts as a proxy and facilitates the entitlement flow between Programmers and MVPDs by offering secure and consistent interfaces for both parties.

For Programmers, Adobe Pass Authentication provides APIs as part of a **Standard** or a **Premium** tier:

* Standard Adobe Pass Authentication APIs:
    * [REST API DCR](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)
    * [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/rest-api-v2-apis-overview.md)

* Premium Adobe Pass Authentication APIs:
    * [Reset Temp Pass API](/help/authentication/integration-guide-programmers/features-premium/temporary-access/temp-pass-feature.md#reset-tempass-api-access)
      * [TempPass Feature](/help/authentication/integration-guide-programmers/features-premium/temporary-access/temp-pass-feature.md)
    * [Degradation API](/help/authentication/integration-guide-programmers/features-premium/degraded-access/degradation-feature.md#degradation-api-access)
      * [Degradation Feature](/help/authentication/integration-guide-programmers/features-premium/degraded-access/degradation-feature.md)
    * [Entitlement Service Monitoring API](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-api.md)

For more details on the entitlement flow, refer to the [Programmer Integration Guide](/help/authentication/integration-guide-programmers/programmer-integration-guide-overview.md#entitlement-flow) documentation.

#### Understanding Entitlements {#understanding-entitlements}

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

#### Building the User Interface {#building-user-interface}

Programmers are responsible for designing and implementing the user interface (UI) for the entitlement workflow within their website or app, while certain elements, such as the login process, are handled by the Pay TV provider.

At a minimum, Programmers must:

* **Implement a provider selection interface**
  * Allow new users to identify their Pay TV provider and log in for the first time.
  * Some Pay TV providers redirect users to an external login page, while others require login within an iframe. Programmers must implement a callback function to generate the iframe when needed.

* **Manage a list of supported Pay TV providers**
  * Ensure users can only access content through approved providers.

* **Indicate authentication status**
  * Show when a user is authenticated within the app or website.

* **Identify protected resources**
  * Clearly indicate which content requires authorization before viewing.
  * Update the UI to reflect successful authorization once access is granted.

## FAQ {#faqs}

**What is TV Everywhere?**

TV Everywhere is an industry initiative that allows Pay TV customers to access the premium content they already subscribe to across various internet-connected devices. This includes personal computers, tablets, smartphones, game consoles, set-top boxes, and Smart TVs. The main challenge is ensuring a seamless and user-friendly authentication process, enabling customers to access their subscription content without multiple logins or technical barriers.

**What is Adobe Pass Authentication, and how does it support TV Everywhere?**

Adobe Pass Authentication brings TV Everywhere to life by securely verifying a user’s entitlement to content in a simple and efficient manner. It is a hosted service that facilitates rapid back-end integration based on business rules set by both Programmers and Pay TV providers. This results in faster time to market for all stakeholders, a more secure environment that minimizes fraud, and a better user experience, with more TV content accessible across multiple platforms.

**How is Adobe Pass Authentication delivered?**

Adobe Pass Authentication is provided as a Software as a Service (SaaS) solution. This approach ensures secure communication between end users, Programmers, and Pay TV providers for content entitlement validation.

**What makes Adobe Pass Authentication different from other TV Everywhere solutions?**

Adobe Pass Authentication offers several advantages over alternative solutions:

* **Seamless Single Sign-On (SSO)** – Unlike direct integrations with individual providers, Adobe Pass Authentication enables a persistent login experience as users move between different websites and apps.
* **Broad Market Penetration** – Once a Programmer integrates with Adobe Pass Authentication, they immediately gain access to Pay TV operators covering over 90% of U.S. households.
* **Integration with Adobe’s Ecosystem** – Works seamlessly with other Adobe solutions for content delivery, protection, and monetization, including Adobe Analytics.

**How secure is Adobe Pass Authentication?**

Security is a top priority. Adobe Pass Authentication ensures that only authorized users can access premium content by binding access to the user’s device. It also provides options for limiting the number of concurrent streams, sessions, or devices per household.

**Which devices does Adobe Pass Authentication support?**

Adobe Pass Authentication is designed to work on a wide range of devices such as web-based devices, mobile devices or TV connected devices.

**Does Adobe Pass Authentication cost anything for end users?**

No. Adobe Pass Authentication is free for end users.
