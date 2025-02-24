---
title: Adobe Pass Authentication 2.63 Release Notes
description: Adobe Pass Authentication 2.63 Release Notes
exl-id: 40987328-6d41-4948-aa4a-bab31f98a18a
---
# Adobe Pass Authentication 2.63 Release Notes {#authn-263-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-263}

* [Build Number](#build-number-263)
* [Release Overview](#release-overview-263)

### Build Number {#build-number-263}

Adobe Pass Authentication: adobe-pass-**2.63**

Release Date: **09/20/2022 - 09/22/2022** 

### Release Overview {#release-overview-263}

#### Improve platform identification mechanism

*   Starting with this release, we improved the mechanism used to identify a device, and will no longer be dependent of the client side implementation. This will provide a more accurate granularity when applying business rules at platform level, and a better understanding of traffic values in ESM reports.

*   A new ESM release will follow soon, with new and improved reports that expose the platform-related fields.

*   For more details about the planned changes, please reach out to your TAM.

#### MVPD self-degradation

This feature provides MVPDs with the capability to temporarily bypass their own authentication and authorization endpoints for high traffic scenarios when the load on those respective end-points becomes too high.

#### Add proxied ID in the header of the authorization calls

This feature adds the id of a Synacor proxied MVPD in the authorization call's header. That enables Synacor to setup business rules for each individual proxied (ex. routing to different domains per proxied MVPD).

#### TVE Dashboard

In this release we fixed an issue where authN or authZ TTL set at MVPD level were not correctly computed in the configuration reports.

#### JavaScript SDK 4.6.0

* Removed the usage of `eval` function, thus making the SDK compliant with Content Security Policy. 
* Fixed an issue that prevented the Authentication flow from finishing with success when the browser's Local Storage was explicitly cleared by a Partner Application.
