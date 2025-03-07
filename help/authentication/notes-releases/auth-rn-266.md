---
title: Adobe Pass Authentication 2.66 Release Notes
description: Adobe Pass Authentication 2.66 Release Notes
exl-id: 7c3cd007-ed2b-455f-8f70-6ec5d0a6552a
---
# Adobe Pass Authentication 2.66 Release Notes {#authn-266-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-266}

* [Build Number](#build-number-266)
* [Release Overview](#release-overview-266)

### Build Number {#build-number-266}

Adobe Pass Authentication: adobe-pass-**2.66.0.1**

Release Date: **07/11/2023 - 07/13/2023** 

### Release Overview {#release-overview-266}

With this release we continued internal updates for the new REST API.
 
#### Bug Fixes

* Fixed the logout flow for SAML based MVPDs, where RelayState parameter was missing from the logout request. We'll target configuration updates after the release to restore the logout flow for affected MVPDs.
* Added the capability to update SSL certificates in our configuration for SOAP authorization endpoints.
* Fixed a corner case where incorrect data was logged in the Programmer field in some ESM reports.
