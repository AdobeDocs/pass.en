---
description: For live/linear content, TVSDK replaces a chunk of the main stream content with an ad break of the same duration, so that the timeline duration remains the same.
title: Live/linear ad resolving and insertion
exl-id: b0fbdddf-8529-4f7a-aef2-1764320307f1
---
# Live/linear ad resolving and insertion{#live-linear-ad-resolving-and-insertion}

For live/linear content, TVSDK replaces a chunk of the main stream content with an ad break of the same duration, so that the timeline duration remains the same.

Before and during playback, TVSDK resolves known ads, replaces parts of the main content with ad breaks of the same duration, and recomputes the virtual timeline, if necessary. The positions of the ad breaks are specified by cue points that are defined by the manifest.

TVSDK inserts ads in the following ways:

* **Pre-roll**, which is at the beginning of the content. 
* **Mid-roll**, which is in the middle of the content.

TVSDK accepts the ad break even if the duration is longer or shorter than the cue point replacement duration. By default, TVSDK supports the `#EXT-X-CUE` cue as a valid ad marker when resolving and placing ads. This marker requires the metadata field `DURATION` in seconds and the cue's unique ID. For example: 

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>When implementing a customary `AdPolicySelector`, a different policy can be given to pre-roll, mid-roll, and post-roll `AdBreakTimelineItem`s in `AdPolicyInfo`, which is based on the type of the `AdBreakTimelineItem`s. For example, you can keep mid-roll content after it has played but remove pre-roll content after it is played.

After playback starts, the video engine periodically refreshes the manifest file. TVSDK resolves any new ads and inserts the ads when a cue point is encountered in the live or linear stream that was defined in the manifest. After ads are resolved and inserted, TVSDK computes the virtual timeline again and dispatches a `TimelineEvent.TIMELINE_UPDATED` event.
