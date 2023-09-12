---
description: For video-on-demand (VOD) content, TVSDK inserts ad breaks by splicing the ads in the main content so that the timeline duration increases.
title: Resolve and insert VOD ad
exl-id: c8e1423c-5d53-452c-ad01-8335ccf42471
---
# Resolve and insert VOD ads {#resolve-and-insert-vod-ad}

For video-on-demand (VOD) content, TVSDK inserts ad breaks by splicing the ads in the main content so that the timeline duration increases.

Before playback, TVSDK resolves known ads, inserts ad breaks in the main content as described by a timeline that is returned from Adobe Primetime ad decisioning, and recomputes the virtual timeline, if necessary.

TVSDK inserts ads in the following ways:

* **Pre-roll**, which is placed before the content. 
* **Mid-roll**, which is in the middle of the content. 
* **Post-roll**, which is placed after the content.

>[!TIP]
>
>After playback starts, no additional changes can occur in the content.

Ads cannot be:

* Inserted 
* Deleted

  For example, you cannot delete built-in ads from the content to offer an ad-free experience. 
* Replaced

  For example, you cannot replace built-in ads with targeted ads.
