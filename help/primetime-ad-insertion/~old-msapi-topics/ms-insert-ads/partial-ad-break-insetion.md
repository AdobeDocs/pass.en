---
description: The Partial Ad Break Insertion (PABI) feature mimics a TV like experience in which if the user joins a live stream inside a mid-roll break, the user is shown mid-roll ads instead of a pre-roll ad or slate.
title: Partial Ad Break Insertion
---

# Partial Ad Break Insertion {#partial-ad-break-insertion}

The Partial Ad Break Insertion (PABI) feature mimics a TV like experience in which if the user joins a live stream inside a mid-roll break, the user is shown mid-roll ads instead of a pre-roll ad or slate.

When the ad server returns pre-roll ads for a live stream, the manifest server will inject the pre-roll ad break before the live-point and insert the EXT-X-START tag with its TIMEOFFSET value pointing to the start of the pre-roll ad break. This default behavior ensures the entire pre-roll ad break is played before the content at the live-point. If a user joins a stream when the live-point is near a mid-roll ad break, the user will be shown the pre-roll ad break before the mid-roll ad break at the live-point.

The PABI feature instructs the manifest server ignore the pre-roll ad break and set the EXT-X-START:TIMEOFFSET value to the beginning of the mid-roll ad present at live-point. This ensures the user sees the entire mid-roll ad currently playing at the live-point without having to view the pre-roll ad break.

>[!NOTE]
>
>This functionality is only available for live streams. The manifest server inserts the pre-roll ad break atop the VOD playlist by default.

>[!NOTE]
>
>To enable PABI, you will need to specify the [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) in the bootstrap URL.

>[!NOTE]
>
>The [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) is a standard HLS tag that indicates a preferred starting point within the playlist.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Use client-side tracking because the client has more control over the firing of tracking beacons. 
* Partial ad breaks should only be used with server-side tracking mode if the player supports EXT-X-START.