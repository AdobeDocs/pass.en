---
description: You can obtain a description of the timeline associated with the currently selected item being played by TVSDK. This is most useful when your application displays a custom scrub-bar control in which the content sections that correspond to ad content are identified.
title: Inspect the playback timeline
exl-id: af373f1e-ed5b-40a9-a91e-9eb0e4a181de
---
# Inspect the playback timeline{#inspect-the-playback-timeline}

You can obtain a description of the timeline associated with the currently selected item being played by TVSDK. This is most useful when your application displays a custom scrub-bar control in which the content sections that correspond to ad content are identified.

Here is an example implementation as seen in the following screen shot.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Access the `Timeline` object in the `MediaPlayer` using the `getTimeline` method.

   The `Timeline` class encapsulates the information that is related to the contents of the timeline that is associated with the media item that is currently loaded by the `MediaPlayer` instance. The `Timeline` class provides access to a read-only view of the underlying timeline. The `Timeline` class provides a getter method that provides  an iterator through a list of `TimelineMarker` objects. 

1. Iterate through the list of `TimelineMarkers` and use the returned information to implement your timeline.

       A `TimelineMarker` object contains two pieces of information:

    * Position of the marker on the timeline (in milliseconds)
    * Duration of the marker on the timeline (in milliseconds)

1. Implement the listener callback interface `MediaPlayer.PlaybackEventListener.onTimelineUpdated` and register it with the `Timeline` object.

   The `Timeline` object can inform your application about changes that might occur in the playback timeline by calling your `OnTimelineUpdated` listener.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```
