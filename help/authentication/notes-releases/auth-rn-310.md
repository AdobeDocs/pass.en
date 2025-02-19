---
title: Adobe Pass Authentication 3.1.0 Release Notes
description: Adobe Pass Authentication 3.1.0 Release Notes
---
# Adobe Pass Authentication 3.1.0 Release Notes {#authn-310-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-310}

* [Build Number](#build-number-310)
* [Release Overview](#release-overview-310)

### Build Number {#build-number-310}

Adobe Pass Authentication: adobe-pass-**3.1.0**

Release Date: **02/25/2025 - 02/27/2025**

### Release Overview {#release-overview-310}

#### REST API v2

* New `partner_logout` action name and `partner_interactive` action type to differentiate between regular logout and partner single sign-on logout in REST API v2 [Logout API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) response.
* New `reason` field to provide more insights into the action name in REST API v2 [Sessions API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) and [Sessions SSO API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md) responses.

#### Bug Fixes

* Fixed an issue that prevented Spectrum subscribers to authenticate through the REST API v2 [Authenticate API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md).
* Fixed an issue that prevented events generated via REST API V2 [Authenticate API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md) from being properly aggregated in ESM.
* Fixed an issue that caused wrong computation of `notBefore` timestamp for the user profiles in REST API v2 [Profiles API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) response.

#### JavaScript SDK

* Removed version 3.5.0 of [AccessEnabler JavaScript SDK](authn-rn-javascript-471.md).