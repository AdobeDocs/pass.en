---
description: Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.
title: Repackage incompatible ads using Adobe Creative Repackaging Service (CRS)
exl-id: b6fb2846-64b6-4db7-a6a9-f85365780775
---
# Repackage incompatible ads using Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.

Ads served from various third parties, such as an agency ad server, your inventory partner, or an ad network, are often delivered in incompatible formats, such as the progressive download MP4 format.

When TVSDK first encounters an incompatible ad, the player ignores the ad and issues a request to the creative repackaging service (CRS), which is part of the Primetime ad insertion back end, to repackage the ad into a compatible format. CRS attempts to generate multiple bit rate M3U8 renditions of the ad and stores these renditions on the Primetime Content Delivery Network (CDN). The next time TVSDK receives an ad response that points to that ad, the player uses the HLS-compatible M3U8 version from the CDN.

To activate this optional CRS feature, contact your Adobe representative. 

>[!NOTE]
>
>For CRS Version 3.0 (and earlier) customers, beginning with CRS Version 3.1 the following changes have improved both security and performance:
>
>* CRS 3.1 continues with `https:` if the content being repackaged uses `https:`. This reduces the potential for some players to present unsecure content.
>
>* CRS 3.1 greatly minimizes network calls, improving video startup time.
>

For more information about CRS, see [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## Enable CRS in TVSDK applications{#enable-crs-in-tvsdk-applications}

To enable CRS in your TVSDK applications, you must set the following information in your Auditude settings:

1. Enable CRS in `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
