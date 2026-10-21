---
title: Adobe Pass Authentication 3.10.0 Release Notes
description: Adobe Pass Authentication 3.10.0 Release Notes
hold: true
product_v2:
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
    internal-label: Pass
---
# Adobe Pass Authentication 3.10.0 Release Notes {#authn-3100-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-3100}

* [Build Number](#build-number-3100)
* [Release Overview](#release-overview-3100)

### Build Number {#build-number-3100}

Adobe Pass Authentication: adobe-pass-**3.10.0**  
Release Date: **10/27/2026 - 10/29/2026**

### Release Overview {#release-overview-3100}

This release focuses on Single Sign-On controls, user metadata enhancements, and reliability improvements for REST API V2 and MVPD configuration management.

#### Enhancements

* Added integration-level control for Service Token Single Sign-On (SSO). Service Token SSO is used only when explicitly enabled for the integration.
* Added support for custom user metadata (for example, `packageType`) during authentication, authorization, and preflight. REST API V2 authorization and preflight decisions now include configured user metadata, including cached responses, while respecting metadata access and encryption settings.

#### Bug Fixes

* Fixed an issue that caused REST API V2 Apple SSO profile requests to fail with an invalid SAML response error for integrations using OAuth2 MVPDs through SAML.
* Fixed an issue where preflight and authorization decisions for the same resource could overwrite each other's cached expiration times and user metadata.
* Fixed an issue where deleting proxied MVPDs left unreferenced platform settings that prevented subsequent configuration saves.
