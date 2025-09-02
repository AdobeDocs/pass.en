---
title: Adobe Pass Authentication 3.4.0 Release Notes
description: Adobe Pass Authentication 3.4.0 Release Notes
exl-id: 7a9b8c6d-4e5f-4a3b-8c7d-9e0f1a2b3c4d
---
# Adobe Pass Authentication 3.4.0 Release Notes {#authn-340-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-340}

* [Build Number](#build-number-340)
* [Release Overview](#release-overview-340)

### Build Number {#build-number-340}

Adobe Pass Authentication: adobe-pass-**3.4.0**
Release Date: **09/09/2025 - 09/11/2025**

### Release Overview {#release-overview-340}

#### REST API v2

* Added support for [Experience Cloud ID (ECID)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-visitor-identifier.md) to improve user identification and tracking capabilities.
* Changed headers AP-Device-Identifier and X-Device-Info to optional for REST API V2 [Configuration API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md).

#### Bug Fixes

* Fixed an issue where MVPD id and Proxy MVPD id were reversed in the token from REST API V2 [Decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) response.
* Fixed an issue where requestor ID was not present in the token from REST API V2 [Decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) response.
* Fixed an issue where passing too many resourced to the REST API V2 [Preauthorize Decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) API resulted in an empty decisions list in the response instead of the [Enhanced Error Code](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) **too_many_resources**.

#### Misc

* Patched security vulnerabilities.