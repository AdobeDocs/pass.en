---
description: The creative repackaging service (CRS) ensures that a non-HLS ad creative can play back properly in HLS streams. The manifest server calls on CRS when it encounters a non-HLS ad.
title: Overview of CRS
---

# Overview of CRS {#overview-of-crs}

The creative repackaging service (CRS) ensures that a non-HLS ad creative can play back properly in HLS streams. The manifest server calls on CRS when it encounters a non-HLS ad.

>[!NOTE]
>
>By default, CRS is disabled. To enable CRS for your account, contact your Adobe technical account manager. 
>
>For information on enabling CRS within TVSDK apps, see the *Enable CRS in TVSDK applications* topic in the Programmer's Guide for your platform. For example, for Android 3.4, see [Enable CRS in TVSDK applications](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS prepares HTTP Live Streaming (HLS) ad creatives for the content stream and injects ID3 packets for client-side ad tracking. It transcodes MP4, FLV, and WebM files received from third-party ad servers, ad networks, and agency servers into HLS format.

When Adobe Primetime ad insertion encounters a non-HLS ad creative, it sends it to CRS for repackaging, which typically takes no longer than three minutes. CRS sends the transcoded ad creative to the CDN server for future use. This is called **`just-in-time (JIT) repackaging`**. You can also transcode ad creatives before they're needed using the  [Repackaging API](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . This is called *`asynchronous repackaging`*.

Your Adobe technical account manager can also change some CRS default behaviors if another behavior is better suited to your application. These are:

* Priority of ad creative formats.

  The `MediaFiles` section of a VAST/VMAP response can contain creatives with different `MediaFile` types. By default the manifest server selects one according to a fixed set of priorities ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe can change the priorities for your account. 
* Ad target duration.

  The manifest server detects the target ad duration from the content playlist and sends it to CRS. Adobe can change this behavior so that CRS always uses a fixed duration that you specify for your account.
