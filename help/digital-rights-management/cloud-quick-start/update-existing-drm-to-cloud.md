---
title: Update existing DRM content to use Cloud DRM (Optional)
description: Update existing DRM content to use Cloud DRM (Optional)
copied-description: yes
exl-id: 89b1e99a-cb28-4524-9c47-f71f92d3753d
---
# Update existing DRM content to use Cloud DRM (Optional) {#update-existing-drm-content-to-use-cloud-drm-optional}

If you have an existing library of content protected by Primetime DRM, it is possible to "re-header" the existing content to use the  Primetime Cloud DRM service, instead of having to re-package/encrypt the original source files. Re-headering the content simply updates the DRM Metadata of the content in the HLS manifest. It does not perform any unencryption/re-encryption of the original asset. This may be a useful option if the original source content is not available, or if there is concern over the amount of resources required to re-package a large library.

It is possible to use the Primetime DRM Java SDK to update the metadata programmatically. In addition, the [!DNL OfflinePackager.jar] command-line tool included with this Protection Kit can also accomplish this task using the `-drm_refresh` option.

## Re-Header Details {#section_3F3980D8E775450588C64E02A8448189}

Re-headering must update the following fields to use CloudDRM:

* License Server URL (To [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod]) 
* License Server Certificate (To the CloudDRM license server certificate) 
* Transport Certificate (To the CloudDRM transport certificate) 
* Packager Credential (To the packager credential you have activated for use with CloudDRM)

## Finding the DRM Metadata {#section_28721CB7966F40708AEC8637F2E9BB72}

Content that uses HTTP technology (such as HDS or HLS) utilizes a manifest that references the Adobe Access DRM metadata. In HDS, the metadata is referenced by the `<drmmeta>` tag, and in HLS, it is referenced by the `#EXT-X-FAXS-CM` tag. In either scenario, the metadata can be contained inline in the manifest as a base-64 encoded blob, or referenced externally as a binary file. If the metadata is embedded/inline in the manifest, you may have to first base64-decode the metadata into binary data before using that data to instantiate DRM metadata.  

## Using the included OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

Supply the `-drm_refresh option` to the command line. A new manifest file will be created with updated DRM Metadata, while the content will not be re-encrypted.  

## Using the Primetime DRM Java SDK to Re-header {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

Updating an existing DRM Metadata can be accomplished by using the Primetime DRM (formerly known as Adobe Access DRM) Java SDK for a programmatic approach. For more details, please refer to the [!DNL RegenerateMetadata.java] code sample in the [!DNL /Reference Implmentation/Command Line Tools/samples/] package of the SDK. The Adobe Access Java SDK is not a part of this CloudDRM Protection Kit, and must be acquired directly from Adobe. Please contact your Adobe business contact for further details.
