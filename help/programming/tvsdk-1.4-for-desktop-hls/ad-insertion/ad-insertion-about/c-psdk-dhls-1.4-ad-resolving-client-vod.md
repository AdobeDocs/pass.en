---
description: For video-on-demand (VOD) content, TVSDK inserts ad breaks by splicing the ads in the main content so that the timeline duration increases.
title: VOD ad resolving and insertion
exl-id: 6f02c7fc-028d-442f-92d4-9efa671b7f02
---
# VOD ad resolving and insertion{#vod-ad-resolving-and-insertion}

For video-on-demand (VOD) content, TVSDK inserts ad breaks by splicing the ads in the main content so that the timeline duration increases.

Before playback, TVSDK resolves known ads, inserts ad breaks in the main content as described by a timeline that is returned from TVSDK, and recomputes the virtual timeline, if necessary.

TVSDK inserts ads in the following ways:

* **Pre-roll**, which is before the content. 
* **Mid-roll**, which is in the content. 
* **Post-roll**, which is after the content.

>[!IMPORTANT]
>
>When implementing a custom `AdPolicySelector`, a different policy can be given to each type of `AdBreakTimelineItem` (pre-roll, mid-roll, or post-roll) in `AdPolicyInfo`, based on the type of the `AdBreakTimelineItem`. For example, you can keep mid-roll content after it has played but remove pre-roll content after it has played.

After playback starts,  no additional changes can occur in the content. Ads cannot be:

* Inserted 
* Deleted

  For example, you cannot delete built-in ads from the content to offer an ad-free experience. 
* Replaced

  For example, you cannot replace built-in ads with targeted ads.
