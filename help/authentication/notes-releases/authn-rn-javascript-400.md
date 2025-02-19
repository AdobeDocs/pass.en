---
title: Adobe Pass Authentication JavaScript 4.0.0 Release Notes
description: Adobe Pass Authentication JavaScript 4.0.0 Release Notes
exl-id: 2ded9ad8-56f7-44b5-87a2-12a195cd0829
---
# Adobe Pass Authentication JavaScript 4.0.0 Release Notes {#javascript-sdk-400-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Build Number {#build-number-400}

Adobe Pass Authentication: JavaScript 4.0.0

Release Date: **07/05/2018**

## Release Overview {#release-overview-400}

* Implemented support for dynamic client registration mechanism, a unified security mechanism across platforms. Managing security access across platforms can be done via TVE dashboard, by the programmer itself.
* Eliminates the usage of all 3rd party cookies and almost all 1st party cookies for all functionalities (except individualization where a 1st party cookie is still used - will be removed in the future), thus making it more compatible and future-proof with emerging browser policies around 3rd party cookies, or cookies in general (eg. Safari's ITP). Note that the previous 3.x release does work as expected for the happy flows by using only 1st party cookies, but this might change with the release of new browser versions.
* Support for disabling caching for preflight authorization checks.
* This version is NOT backwards compatible, and is hosted under a new path: https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js . In order to benefit from this new JS SDK a migration process is needed from Programmers in order to register their web applications using the new dynamic client registration mechanism and to point to the new JS SDK url.

## Release Package {#release-package-400}

The production URL is: https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js

The staging URL is: https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js
