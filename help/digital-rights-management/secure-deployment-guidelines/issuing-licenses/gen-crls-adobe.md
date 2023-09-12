---
description: You can use Adobe Primetime DRM to create CRLs that supplement the machine CRL that is published by Adobe.
title: Generating CRLs to supplement those published by Adobe
---

# Generating CRLs to supplement those published by Adobe{#generating-crls-to-supplement-those-published-by-adobe}

You can use Adobe Primetime DRM to create CRLs that supplement the machine CRL that is published by Adobe.

The Primetime DRM SDK checks and enforces the Adobe CRLs. However, you can disallow additional client machines by creating a CRL that revokes additional machine credentials by passing the CRL to the Primetime DRM SDK. When you issue a license, the SDK checks the Adobe CRL and your CRL.

To generate CRLs, see [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html). 
