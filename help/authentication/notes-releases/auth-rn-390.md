---
title: Adobe Pass Authentication 3.9.0 Release Notes
description: Adobe Pass Authentication 3.9.0 Release Notes
hold: true
---
# Adobe Pass Authentication 3.9.0 Release Notes {#authn-390-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-390}

* [Build Number](#build-number-390)
* [Release Overview](#release-overview-390)

### Build Number {#build-number-390}

Adobe Pass Authentication: adobe-pass-**3.9.0.1**  
Release Date: **09/08/2026 - 09/10/2026**

### Release Overview {#release-overview-390}

This release focuses on REST API V2 and ESM metrics improvements.

#### Enhancements

* Improved REST API V2 Partner Single Sign-On to ensure a valid authentication request is returned for MVPDs configured with OAuth2.
* Improved REST API V2 Decisions to return a clear error response when authorization fails, instead of an empty response.
* Improved registration code generation to prevent visually ambiguous characters, making codes easier to read and enter correctly.
* ESM Dashboard enhancements with support for Preflight AuthZ Metrics.
