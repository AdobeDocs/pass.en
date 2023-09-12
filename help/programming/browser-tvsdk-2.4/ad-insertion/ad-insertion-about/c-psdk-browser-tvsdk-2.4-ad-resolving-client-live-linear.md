---
description: For live/linear content, Browser TVSDK replaces a chunk of the main stream content with an ad break of the same duration, so that the timeline duration remains the same.
title: Live/linear ad resolving and insertion
exl-id: 5d5954c6-9d1c-4900-9813-d3248fd61911
---
# Live/linear ad resolving and insertion{#live-linear-ad-resolving-and-insertion}

For live/linear content, Browser TVSDK replaces a chunk of the main stream content with an ad break of the same duration, so that the timeline duration remains the same.

Before and during playback, Browser TVSDK resolves known ads, replaces parts of the main content with ad breaks of the same duration, and recomputes the virtual timeline, if necessary. The positions of the ad breaks are specified by cue points that are defined by the manifest.

Browser TVSDK inserts ads in the following ways:

* **Pre-roll**, which is at the beginning of the content.

Browser TVSDK accepts the ad break even if the duration is longer or shorter than the cue point replacement duration. By default, Browser TVSDK supports the `#EXT-X-CUE` cue as a valid ad marker when resolving and placing ads. This marker requires the metadata field `DURATION` in seconds and the cue's unique ID. For example: 

```
#EXT-X-CUE:DURATION=27,ID="..."
```

You can define and subscribe to additional cues (tags).

After playback starts, the video engine periodically refreshes the manifest file. Browser TVSDK resolves any new ads and inserts the ads when a cue point is encountered in the live or linear stream that was defined in the manifest. After ads are resolved and inserted, Browser TVSDK computes the virtual timeline again and dispatches a `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` event.

>[!TIP]
>
>For live streams, Browser TVSDK supports only MP4 and HLS pre-roll and mid-roll ads.
