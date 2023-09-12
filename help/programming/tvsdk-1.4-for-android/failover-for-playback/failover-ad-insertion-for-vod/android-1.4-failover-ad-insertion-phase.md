---
description: TVSDK inserts the alternate content (ads) into the timeline that corresponds to the main content.
title: Ad-insertion phase
exl-id: bad246e9-ff2b-4584-a320-826385bb0e6d
---
# Ad-insertion phase{#ad-insertion-phase}

TVSDK inserts the alternate content (ads) into the timeline that corresponds to the main content.

When the ad-resolving phase is complete, TVSDK has an ordered list of ad resources that are grouped into ad breaks. Each ad break is positioned on the main content timeline using a start-time value that is expressed in milliseconds (ms). Each ad in an ad break has a duration property that is also expressed in ms. The ads in an ad break are chained together one after another. As a result, the duration of an ad break is equal to the sum of the durations of the individual composing ads.

Failover can occur in this phase with conflicts that might occur on the timeline during ad insertion. For specific combinations of ad break start-time/duration values, ad segments might overlap. The overlap occurs when the last portion of an ad break intersects the beginning of the first ad in the next ad break. In these situations, TVSDK discards the later ad break and continues the ad-insertion process with the next item on the list until all ad breaks are inserted or discarded.

TVSDK issues a warning notification about the error and continues processing.
