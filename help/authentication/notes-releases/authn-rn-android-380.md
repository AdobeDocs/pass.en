---
title: Adobe Pass Authentication Android 3.8.0 Release Notes
description: Adobe Pass Authentication Android 3.8.0 Release Notes
---
# Adobe Pass Authentication Android 3.8.0 Release Notes {#android-sdk-380-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Build Number {#build-number-380}

Adobe Pass Authentication: Android 3.8.0

Release Date: **09/18/2025**

## Release Overview {#release-overview-380}

* Fix a vulnerability with the SDK's storage broadcast receiver. A malicious application may present a false link to interrogate the shared storage for the Adobe tokens.
  However, no critical information is stored, and the likelihood that any user was impacted by this vulnerability is very low.
  * Note: As a result of the change, users will be logged out.
  
## Release Package {#release-package-380}

You can download Android SDK v3.8.0 from [here](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library).
