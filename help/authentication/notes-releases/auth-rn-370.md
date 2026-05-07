---
title: Adobe Pass Authentication 3.7.0 Release Notes
description: Adobe Pass Authentication 3.7.0 Release Notes
---
# Adobe Pass Authentication 3.7.0 Release Notes {#authn-370-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-370}

* [Build Number](#build-number-370)
* [Release Overview](#release-overview-370)

### Build Number {#build-number-370}

Adobe Pass Authentication: adobe-pass-**3.7.0.2**  
Release Date: **05/12/2026 - 05/14/2026**

### Release Overview {#release-overview-370}

This release focuses on MVPD integration upgrades, bug fixes, and TVE Dashboard improvements.

#### MVPD Integrations

* Added PKCE support for OAuth2-based MVPD authentication.

#### Enhancements

* Released TVE Dashboard version 1.5.1.

#### Bug Fixes

* Fixed an issue that caused Apple SSO to overlook certain MVPD configuration mismatches.
* Fixed an issue that caused HTTP 500 errors on authorization deny due to invalid characters in the response header.
