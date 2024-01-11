---
title: Adobe Pass Authentication JavaScript 4.4.0 Release Notes
description: Adobe Pass Authentication JavaScript 4.4.0 Release Notes
---
# Adobe Pass Authentication JavaScript 4.4.0 Release Notes {#javascript-sdk-440-release-notes}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This page describes new features, changes, and known issues with this release:

## Build Number {#build-no-javascript-sdk-440}

Adobe Pass Authentication: JavaScript 4.4.0

Release Date: **06/22/2021**


## Release Overview {#overview-javascript-sdk-440}

### New Features {#new-features-javascript-sdk-440}

Preflight authorization

* New preauthorize API - this is the new API call to be used for our Preflight Authorization feature, which also introduces enhanced error reporting for preflight flow.
* This feature is available upon request as it has to enabled on Primetime Authentication configuration. Please contact your TAM for additional details on how to enable this feature.
* Deprecates checkPreauthorizedResources API.

Platform identification

* Adds AP-SDK-Identifier header on all SDK calls to better identify SDK type and version.

Others

* Internal architectural improvements.


### Bug Fixes {#bug-fixes-javascript-sdk-440}

* Fix race condition produced when setRequestor and getAuthentication are called simultaneously.
* Fixed an issue that prevented entitlements to be loaded correctly on staging environments.
* Addressed an issue that prevented background logout flow to complete on Safari browsers, thus the user still seemed authenticated until a page refresh occurred. A timeout was introduced, currently set at 30 seconds, so if there's no response from Primetime Authentication server during this period, the SDK will invoke setAuthenticationStatus callback.

## Release package {#rel-pkg-javascript-sdk-440}

The production URL is: https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js

The staging URL is: https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js
