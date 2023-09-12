---
description: You can obtain a description of the timeline associated with the currently selected item being played by TVSDK. This is most useful when your application displays a custom scrub-bar control in which the content sections that correspond to ad content are identified.
title: Inspect the playback timeline
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
---
# Inspect the playback timeline{#inspect-the-playback-timeline}

You can obtain a description of the timeline associated with the currently selected item being played by TVSDK. This is most useful when your application displays a custom scrub-bar control in which the content sections that correspond to ad content are identified.

Here is an example implementation as seen in the following screen shot. 
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. Access the `Timeline` object in the `MediaPlayer` using the `get` method.

   The `Timeline` class encapsulates the information that is related to the contents of the timeline that is associated with the media item that is currently loaded by the `MediaPlayer` instance. The `Timeline` class provides access to a read-only view of the underlying timeline. The `Timeline` class provides a getter method for obtaining all placed `TimelineMarker` objects. 

1. Iterate through the list of `TimelineMarkers` and use the returned information to implement your timeline.

       A `TimelineMarker` object contains two pieces of information:

    * Position of the marker on the timeline (in milliseconds) 
    * Duration of the marker on the timeline (in milliseconds)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```
