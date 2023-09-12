---
description: The manifest server supports publisher-enabled WebVTT captions for all HLS video formats. When it receives requests to insert ads into WebVTT captioned content, it does so correctly.
title: Support for WebVTT captions
---

# Support for WebVTT captions {#support-for-webvtt-captions}

The manifest server supports publisher-enabled WebVTT captions for HLS/DASH video formats. When it receives requests to insert ads into WebVTT captioned content, it does so correctly.

If the publisher includes WebVTT captions in the content, the manifest server sends the client a content stream with captions. WebVTT must be enabled by the publisher for the manifest server to support captions. When the client has WebVTT captions enabled, and sends a request to the manifest server, the manifest server manipulates the timeline and WebVTT track and returns content with stitched ads and captions to the client.

The workflow for VOD content streams is as follows:

1. The client sends a content stream with WebVTT captions enabled to the manifest server.
1. The manifest server manipulates the timeline to stitch ads into the content stream.
1. The manifest server manipulates the WebVTT track to add captions to the content (including ads).
1. The manifest server delivers the content stream to the client, with inserted ads and captions.

>[!NOTE]
>
>If a WebVTT caption segment falls within a mid-roll ad, the viewer sees that caption play before and after that mid-roll ad break. For example, in a 10-second caption segment with a 30-second mid-roll ad at the 5-second mark, the viewer sees that caption segment for 5 seconds before the mid-roll ad break, and for 5 seconds after the mid-roll.

>[!NOTE]
>
>If a client requests that a video play in a specific language such as English, and then requests to play the video in French, manifest server cannot detect that the client requested to change the language to French. Because the client doesn't communicate with the manifest server, the manifest server inserts the ad caption into the video stream using the first language specified in the ad's M3U8 master file.
