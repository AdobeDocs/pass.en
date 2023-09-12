---
description: CRS provides just-in-time (JIT) and asynchronous repackaging and HLS-to-HLS conversion. The result of repackaging is an HLS formatted version of the original ad creative. CRS places the HLS formatted version on the content delivery network (CDN) server for use when needed.
title: Main Uses of CRS
---

# Main Uses of CRS {#main-uses-of-crs}

CRS provides just-in-time (JIT) and asynchronous repackaging and HLS-to-HLS conversion. The result of repackaging is an HLS formatted version of the original ad creative. CRS places the HLS formatted version on the content delivery network (CDN) server for use when needed.

In JIT repackaging Adobe Primetime ad insertion begins the repackaging process when it first encounters a non-HLS ad creative. This usually entails lost opportunities to run the ad during the repackaging process.

In asynchronous repackaging, the ad creative is transcoded and stored before it is needed, which can eliminate those lost opportunities.

In HLS-to-HLS conversion, CRS reformats an HLS ad creative into appropriate sized chunks to ensure consistent playback.

## Just-in-Time Repackaging {#section_1BA344F2300B49F291865A7461EDFEAE}

The sequence for JIT repackaging is as follows:

1. The manifest server fetches an ad.
1. If the ad format is HLS, the manifest server inserts the ad into the content stream.
1. If the format is not HLS (for example, MP4, FLV, or WebM), the manifest server looks for a transcoded version on the CDN server. If it finds one, it inserts the transcoded ad into the content stream.
1. If the format is not HLS and the CDN server has no transcoded version, the manifest server passes the ad to CRS, which transcodes the ad creative and stores the result on the CDN server for later use.
1. The manifest server returns the content without the ad.

## Asynchronous Repackaging {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

You can use the API described in [Repackaging API](../~old-creative-repackaging-service/api-repackage.md) to pre-transcode a non-HLS creative to minimize loss of impressions and maximize monetization.

## HLS-to-HLS Conversion {#section_877A0E7E8FAF4C2DB086A31C24D53435}

To avoid buffering and delay, a client downloads a video in small chunks. If the chunk sizes are inconsistent, the playback may be jerky. HLS-to-HLS conversion ensures that data chunks are all of the same duration (for example, 6 seconds).

>[!NOTE]
>
>CRS produces HLS version 3, regardless of which HLS version it receives.