---
description: To receive notifications about timeline updates, register the appropriate event listeners.
title: Add listeners for TimelineUpdatedEvent
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
---
# Add listeners for TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

To receive notifications about timeline updates, register the appropriate event listeners.

 Each time the timeline updates, the `MediaPlayer` dispatches `AdobePSDK.TimelineEvent` with type `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`. 
1. Implement the appropriate listeners.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. Register the event listeners.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
