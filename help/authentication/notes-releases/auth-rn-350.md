---
title: Adobe Pass Authentication 3.5.0 Release Notes
description: Learn about the new features, changes, and known issues with this release.
exl-id: b196f636-26a5-4974-903e-40b5f8b93a24
---
# Adobe Pass Authentication 3.5.0 Release Notes

Last update: Tue Dec 09 2025 00:00:00 GMT+0000 (Coordinated Universal Time)

* Topics:
* Authentication

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](https://experienceleague.adobe.com/en/docs/pass/authentication/product-announcements) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-350}

* [Build Number](#build-number-350)
* [Release Overview](#release-overview-350)

### Build Number {#build-number-350}

Adobe Pass Authentication: adobe-pass-**3.5.0**  
Release Date: **12/09/2025 - 12/11/2025**

### Release Overview {#release-overview-350}

#### REST API v2

* Added a new dimension in ESM ("api") to help customers build reports that would distinguish events based on the implementation type: SDK, REST V1, or REST V2.

#### Bug Fixes

* Fixed an issue where custom degradation messages set in TVE Dashboard were not appearing in REST API V2 error details.
* Fixed an issue in REST API V2 where `authenticated_profile_expired` error code was not returned when authenticated profiles expired.
* Fixed an issue where authorization latency calculations and preflight TTL values were incorrect in REST API V2.
* Fixed an issue where inconsistent response format was returned when DCR token expires.
