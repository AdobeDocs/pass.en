---
title: Generating licenses
description: Generating licenses
copied-description: yes
exl-id: 65c5677d-5a69-46f8-bc14-7af6d14d4dff
---
# Generating licenses {#generating-licenses}

To issue a leaf license to the user, the SDK must decrypt the CEK contained in the content metadata and re-encrypt it for the machine requesting a license. To decrypt the CEK, the server must provide information required to decrypt the key. Call `ContentInfo.setKeyRetrievalInfo()` and provide an `AsymmetricKeyRetrieval` object. If the metadata contains multiple policies, the server must determine which policy to use and call `LicenseRequestMessage.setSelectedPolicy()`. Then call `LicenseRequestMessage.generateLicense()` to generate the license. Using the `License` object that is returned, you may modify the expiration or rights in the license.

If an ExternalKeyRetrieval object is specified in the `ContentInfo` object, then the license server is expected to use the associated CEK ID to fetch the appropriate CEK that will be inserted into the license. For more details on how to use the External CEK workflow, see [Adobe Access DRM External CEK Overview](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
