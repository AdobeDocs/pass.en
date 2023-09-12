---
description: An allow list is a list of trusted entities.
title: Maintain an allow list of trusted content packagers
---

# Maintain an allow list of trusted content packagers {#maintain-a-allowlist-of-trusted-content-packagers}

A allow list is a list of trusted entities.

For content packagers, the entities are organizations that are trusted by the content owner to package (or encrypt) the video files and create DRM protected content. When deploying Adobe Primetime DRM, you should maintain an allow list of trusted content packagers. You must also verify the identity of the content packager in the DRM metadata of a DRM protected file before issuing a license.

To learn how to obtain information about the entity that packaged the content, see [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
