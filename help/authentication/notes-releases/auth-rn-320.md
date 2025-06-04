---
title: Adobe Pass Authentication 3.2.0 Release Notes
description: Adobe Pass Authentication 3.2.0 Release Notes
exl-id: 43aee317-dbac-4000-893e-839ee3e9f6ba
---
# Adobe Pass Authentication 3.2.0 Release Notes {#authn-320-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-320}

* [Build Number](#build-number-320)
* [Release Overview](#release-overview-320)

### Build Number {#build-number-320}

Adobe Pass Authentication: adobe-pass-**3.2.0**

Release Date: **06/10/2025 - 06/12/2025**

### Release Overview {#release-overview-320}

#### REST API v2

* A new reason `missing_parameters_fallback` has been added for cases when parameters are missing on [Sessions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) response.
* A new field "device" has been added to [Sessions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md) response.

#### New Features

* Expand Degradation API to add the capability to apply degradation rules for multiple MVPDs in a single call

#### Bug Fixes

* Fixed an issue that prevented the authentication flow to finish successfully in cases where user metadata processing failed.
* Fixed an issue where authorization reason was not correctly computed.
* Fixed an issue where upstreamUserID was not present in the profile response.
* Fixed an issue that caused the authentication request not to include scoping information for REST API V2 initiate authentication requests.
