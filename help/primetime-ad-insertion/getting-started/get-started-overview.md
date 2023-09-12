---
title: Get started with Adobe Primetime Ad Insertion
description: Getting started with Adobe Primetime Ad Insertion
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
---
# Get started with Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion co-ordinates the systems that provide content and ads to create personalized, in-stream ad experiences and then track ad playback for your advertisers.

Primetime Ad Insertion interacts with video-delivery client applications by re-writing video manifests to provide targeted ads and personalized experiences for each viewer. These manifests combine content and ads delivered from an ad server and can optionally include metadata containing detailed ad-tracking instructions. Primetime Ad Insertion supports both client-side and server-side ad tracking.

After the system has been properly set up, a typical workflow might look as follows:

1. The client application generates a [Bootstrap URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) with information about the video stream and sends a GET request to Primetime Ad Insertion.  Primetime Ad Insertion supports HLS and DASH with a variety of ad signaling formats.

1. Primetime Ad Insertion responds by sending the content manifest from the publisher’s CDN back to the client application.

1. The client application chooses appropriate streams in the generated manifest to play and makes requests to Primetime Ad Insertion.

1. Primetime Ad Insertion fetches the requested stream(s) from the content CDN, parses/reads any cue information, makes calls to the ad server and replaces ad breaks as necessary.

1. Primetime Ad Insertion normalizes the manifest by rewriting resource URLs and detecting whether ad creatives require transcoding, see [Just-in-time Ad Transcoding](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime Ad Insertion fetches the required ad creatives and inserts the appropriate fragments into the manifests.

1. Primetime Ad Insertion delivers the final stitched manifests, including ads, to the client application for playback.

1. Ad delivery and viewability can be measured via either client or server-side ad tracking, see [Setting up Ad Tracking](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

Primetime Ad Insertion supports most HLS/DASH client and player configurations. For more information regarding specific ad signaling formats supported please see [Supported cue formats](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
