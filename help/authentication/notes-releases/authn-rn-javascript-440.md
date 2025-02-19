---
title: Adobe Pass Authentication JavaScript 4.4.0 Release Notes
description: Adobe Pass Authentication JavaScript 4.4.0 Release Notes
exl-id: 28cc0ccc-7a1d-45bd-8455-26cfde25c5c5
---
# Adobe Pass Authentication JavaScript 4.4.0 Release Notes {#javascript-sdk-440-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Build Number {#build-number-440}

Adobe Pass Authentication: JavaScript 4.4.0

Release Date: **06/22/2021**

## Release Overview {#release-overview-440}

### New Features

Preflight authorization

* New preauthorize API - this is the new API call to be used for our Preflight Authorization feature, which also introduces enhanced error reporting for preflight flow.
* This feature is available upon request as it has to enabled on Primetime Authentication configuration. Please contact your TAM for additional details on how to enable this feature.
* Deprecates checkPreauthorizedResources API.

Platform identification

* Adds AP-SDK-Identifier header on all SDK calls to better identify SDK type and version.

Others

* Internal architectural improvements.

### Bug Fixes

* Fix race condition produced when setRequestor and getAuthentication are called simultaneously.
* Fixed an issue that prevented entitlements to be loaded correctly on staging environments.
* Addressed an issue that prevented background logout flow to complete on Safari browsers, thus the user still seemed authenticated until a page refresh occurred. A timeout was introduced, currently set at 30 seconds, so if there's no response from Primetime Authentication server during this period, the SDK will invoke setAuthenticationStatus callback.

## Release Package {#release-package-440}

The production URL is: https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js

The staging URL is: https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js
