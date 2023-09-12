---
description: You can specify whether to allow playback before all ads are loaded and placed in the timeline. Starting playback in this way gives a viewer faster access to the main content. This feature is applicable only for live DVR and does not work on, say VOD assets.
title: Enable lazy ad loading
exl-id: 6b70a7ae-28ce-4a19-9560-26e937c721cd
---
# Enable lazy ad loading{#enable-lazy-ad-loading}

You can specify whether to allow playback before all ads are loaded and placed in the timeline. Starting playback in this way gives a viewer faster access to the main content. This feature is applicable only for live DVR and does not work on, say VOD assets.

1. Use the Boolean property `delayAdLoading` in `AdvertisingMetadata`.

    * When false, TVSDK waits until all ads are resolved and placed before transitioning to the PREPARED status. It is false by default. 
    * When true, TVSDK resolves only the initial ads and transitions to the PREPARED status. The remaining ads are resolved and placed during playback.

1. To also activate delayed ad loading with Adobe Primetime ad decisioning, set this to `true` when you create `AuditudeSettings`.

   The `AuditudeSettings` class inherits this property from `AdvertisingMetadata`, but does not inherit the current value.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. To accurately reflect ads as cues on a scrub bar, listen for the `TimelineEvent`. `TIMELINE_UPDATED` event and redraw the scrub bar every time that you receive this event.

   When VoD streams use delayed ad loading, not all ads are placed on the timeline when your player enters the PREPARED status, so you must explicitly redraw the scrub bar.

   TVSDK optimizes the dispatch of this event to minimize the number of times that you must redraw the scrub bar; therefore, the number of timeline events is not related to the number of ad breaks to be placed on the timeline. For example, if you have five ad breaks, you might not receive exactly five events.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
