---
description: To consume locally generated certificate revocation lists (CRLs) and policy update lists, use Adobe Primetime DRM APIs to verify the signature.
title: Consuming locally generated CRLs
---

# Consuming locally generated CRLs {#consuming-locally-generated-crls}

To consume locally generated certificate revocation lists (CRLs) and policy update lists, use Adobe Primetime DRM APIs to verify the signature.

The following APIs verify that the lists have not been tampered with and that the lists were signed by the correct License Server:

* Call [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) to check the signature before you provide the [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) to any APIs.

  For more information, see [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html). 

* Call [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) to check the signature before providing the `PolicyUpdateList` to any APIs.

  For more information, see [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

