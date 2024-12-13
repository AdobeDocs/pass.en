---
title: Adobe Pass Authentication 3.0 Release Notes
description: Adobe Pass Authentication 3.0 Release Notes
exl-id: 9284151a-8458-44a3-937b-35f379ca0e4e
---
# Adobe Pass Authentication 3.0 Release Notes {#pt-authn-300-rn}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This page describes new features, changes, and known issues with this release:

## Server Side and Web Clients {#server-side-web-clients-300}

* [Build Number](#build-number-300)
* [Release overview](#release-overview-300)

### Build Number {#build-number-2651}

Adobe Pass Authentication: adobe-pass-**3.0**
Release Date: **09/10/2024 - 09/12/2024**

### New Features {#new-features-300}

#### REST API v2 {#rest-apis}

##### Code

* Starting with adobe-pass-**3.0** release, new and existing client applications can integrate or migrate to the new REST API v2 to benefit from the latest Adobe Pass functionalities.

##### Documentation

* To start with the new REST API v2, refer to the following documents:
  * [REST API v2 - APIs - Overview](../integration-guide-programmers/rest-apis/rest-api-v2/apis/rest-api-v2-apis-overview.md)
  * [REST API v2 - Flows - Overview](../integration-guide-programmers/rest-apis/rest-api-v2/flows/rest-api-v2-flows-overview.md)
* The URLs for public documents of REST API v1 have changed, refer to the following documents:
  * [REST API v1 - APIs - Overview](../integration-guide-programmers/legacy/rest-api-v1/rest-api-overview.md)
  * [REST API v1 - APIs - Reference](../integration-guide-programmers/legacy/rest-api-v1/rest-api-reference.md)

##### Tools

* To try the new REST API v2, refer to the new Adobe Pass Authentication page from [Adobe Developer](https://developer.adobe.com/adobe-pass) website.

### Bug Fixes {#bug-fixes-300}

* Fixed an issue with redirect URL parameter not being used when present in the logout request.
