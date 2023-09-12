---
title: Embedding licenses
description: Embedding licenses
copied-description: yes
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
---
# Embedding licenses {#embedding-licenses}

Once content has been encrypted and a license has been pre-generated, the license may be embedded into the encrypted content.

If you want to embed a license, you need to obtain an instance of `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. If you know the type of the encrypted content, use the constructor for `FLVKeyMetaDataUpdater` or `F4VKeyMetaDataUpdater`; otherwise, use `MediaProcessorFactory.getMediaProcessor()` to return an instance based on the file type detected. Then you need to onstruct a `KeyMetaDataCallback` and invoke `modifyKeyMetaData()`. Your callback implementation is then invoked when the DRM metadata is located in the encrypted content. Based on the metadata found, you can choose a license to embed and set the license using `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

See `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` in the Reference Implementation Command Line Tools [!DNL Samples] directory for sample code that demonstrates embedded licenses.

>[!NOTE]
>
>An Adobe Primetime DRM 2.0 client ignores any licenses that are embedded in the content and then attempts to obtain a license from the license server that is specified in the metadata. However, if the metadata indicates that no license server is available, a Primetime DRM 2.0 client needs to be upgraded before you can view the content.
