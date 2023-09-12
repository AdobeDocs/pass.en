---
description: You can use the features of the Primetime Digital Rights Management (DRM) system to provide secure access to your video content. Alternatively, you can use third-party DRM solutions as an alternative to Adobe's integrated Primetime DRM solution.
keywords: DRM;DASH;HLS
title: Primetime DRM interface overview
exl-id: e07c1551-5a9b-4907-94ea-6b7536918b91
---
# Primetime DRM interface overview {#primetime-drm-interface-overview}

You can use the features of the Primetime Digital Rights Management (DRM) system to provide secure access to your video content. Alternatively, you can use third-party DRM solutions as an alternative to Adobe's integrated Primetime DRM solution.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Check with your Adobe representative for the most up-to-date information on the availability of 3rd-party DRM solutions.

The key client-side element of the Primetime digital rights management (DRM) system is the DRM Manager.

Primetime DRM provides a scalable, efficient workflow to implement content protection in TVSDK applications. You protect and manage the rights to your video content by creating a license for each digital media file.

TVSDK supports Primetime DRM integration as custom DRM workflows. This means that your application must implement the DRM authentication workflows before playing the stream by using the Flash DRMManager. To enable this, the MediaPlayer provides you with the DRM manager for authentication.

Refer to the DRM sample player code included in the TVSDK package.

These are the most important API elements for working with DRM:

* A reference in the media player to the DRM manager object that implements the DRM subsystem: 

  ```
  @property (readonly, nonatomic) DRMManager *drmManager
  ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK issues a `PTMediaPlayerItemDRMMetadataChanged` notification when the DRM metadata changes. This metadata is used as input for almost all functions of the `DRMManager` class.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

If the DRM-protected stream is multiple bit-rate (MBR) encoded, the DRM metadata that is used for the variant playlist should be the same as the metadata that is used in all the bit-rate streams.

>[!TIP]
>
>When referencing DRM-protected asset URLs in your iOS app, the query string parameter `?faxs=1` must be appended to the (MBR) set-level M3U8 URL. For example:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

The `faxs=1` query string parameter signals that the content is DRM protected, and triggers the DRM decryption workflow accordingly in the iOS TVSDK. You can also append the `faxs=1` tag on DRM-protected HLS asset URLs that are destined for other platforms; it is observed as required on iOS or treated as a non-op in players on other platforms.

## Implement Primetime DRM in a TSVDK application {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM is integrated into TVSDK, which simplifies implementing content protection in a TVSDK application.

For an overview and details on using Primetime DRM to implement content protection in a TVSDK application, see:

* [Adobe Primetime TVSDK-DRM Workflow (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
