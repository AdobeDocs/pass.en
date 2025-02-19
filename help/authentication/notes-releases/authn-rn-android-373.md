---
title: Adobe Pass Authentication Android 3.7.3 Release Notes
description: Adobe Pass Authentication Android 3.7.3 Release Notes
exl-id: f335357e-c209-428d-af2a-2181551447d4
---
# Adobe Pass Authentication Android 3.7.3 Release Notes {#android-sdk-373-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Build Number {#build-number-373}

Adobe Pass Authentication: Android 3.7.3

Release Date: **09/19/2023**

## Release Overview {#release-overview-373}

* Changes to support Android 14 and applications targeting API level 34
  * Add flag required by [Android 14 runtime-registered broadcasts receivers](https://developer.android.com/about/versions/14/behavior-changes-14#runtime-receivers-exported).
* Fix ChromeCustomTabs not opening for MVPD login on emulator API 32+
  * Note: A workaround for this issue on SDK <3.7.3 is to open Chrome app on emulator and finish setting it up before attempting to do MVPD login

## Release Package {#release-package-373}

You can download Android SDK v3.7.3 from [here](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library).
