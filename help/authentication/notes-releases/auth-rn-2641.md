---
title: Adobe Pass Authentication 2.64.1 Release Notes
description: Adobe Pass Authentication 2.64.1 Release Notes
exl-id: b0edbd90-ebb5-40a7-9034-1699dccfadb5
---
# Adobe Pass Authentication 2.64.1 Release Notes {#authn-264-rn}

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-2641}

* [Build Number](#build-number-2641)
* [Release Overview](#release-overview-2641)

### Build Number {#build-number-2641}

Adobe Pass Authentication: adobe-pass-**2.64.1**

Release Date: **01/31/2023 - 02/02/2023** 

### Release Overview {#release-overview-2641}

This release adds the following:

* The ability to block unsolicited authentication responses from MVPDs where "in_response_to" parameter is missing from the SAML assertion.
* An improved validation over redirect_url parameter in order to comply with security requirements.
* An improved logging of the device information for second screen authentication requests, using information provided from the initial device.
