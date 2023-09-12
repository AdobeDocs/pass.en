---
title: Maintain an allow list of trusted content packagers
description: Maintain an allow list of trusted content packagers
copied-description: yes
exl-id: 4c296d23-75c1-4d0b-a636-31b49e99c753
---
# Maintain an allow list of trusted content packagers {#maintain-a-allowlist-of-trusted-content-packagers}

An **allow list** is a list of trusted entities. In the case of content packagers, these are organizations trusted by the content owner to package (or encrypt) the FLV/F4V video files, creating DRM protected content. When deploying Adobe Access, it is recommended that you maintain an allow list of trusted content packagers, and that you verify the identity of the content packager contained in the DRM metadata (the DRM header) of a DRM protected file prior to issuing a license.

To learn more about obtaining information about the entity that packaged the content, see `V2ContentMetaData.getPackagerInfo()` in the *Adobe Access API Reference*.
