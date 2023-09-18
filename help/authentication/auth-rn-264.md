---
title: Adobe Pass Authentication 2.64 Release Notes
description: Adobe Pass Authentication 2.64 Release Notes
exl-id: 4db21026-a0c2-4e33-b01f-4ccae824a110
---
# Adobe Pass Authentication 2.64 Release Notes {#authn-264-rn}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#ss-web-clients}

* [Build Number](#build-no-264)
* [New Features](#new-featres-264)
* [Bug fixes](#bug-fixes-264)

### Build Number {#build-no-264}

Adobe Pass Authentication: adobe-pass-**2.64**

Release Date: **11/08/2022 - 11/10/2022**

### New Features {#new-featres-264}

* Infrastructure updates, targeted at reducing server response times, improving overall performance of the system.
* Improvements to the new platform identification mechanism.
* Ability to block unsolicited authentication responses from MVPDs where "in_response_to" parameter is missing from the SAML assertion.

### Bug fixes {#bug-fixes-264}

* Fixed incorrect formatting of some legacy TempPass tokens.
* Addressed minor issues on second screen authentication flow.
