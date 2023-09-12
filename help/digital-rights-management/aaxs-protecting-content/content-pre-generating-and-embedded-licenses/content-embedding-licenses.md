---
title: Embedding licenses
description: Embedding licenses
copied-description: yes
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
---
# Embedding licenses {#embedding-licenses}

Once content has been encrypted and a license has been pre-generated, the license may be embedded into the encrypted content.

To embed a license, obtain an instance of `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. If you know the type of the encrypted content, use the constructor for `FLVKeyMetaDataUpdater` or `F4VKeyMetaDataUpdater`; otherwise, use `MediaProcessorFactory.getMediaProcessor()` to return an instance based on the file type detected. Construct a `KeyMetaDataCallback` and invoke `modifyKeyMetaData()`. Your callback implementation will be invoked when the DRM metadata is located in the encrypted content. Based on the metadata found, you can choose a license to embed and set the license using `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

For sample code demonstrating embedded licenses, see `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` in the Reference Implementation Command Line Tools “Samples” directory.

>[!NOTE]
>
>Adobe Access 2.0 clients will ignore any licenses embedded in the content and will attempt to obtain a license from the license server specified in the metadata. However, if the metadata indicates that no license server is available, an Adobe Access 2.0 client will need to upgrade to view the content.

See [Out-of-band Licenses](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
