---
description: This example shows the recommended way to include custom ad markers on the playback timeline.
title: Place custom ad markers on the timeline
exl-id: a5dafca5-5217-4800-a467-ad5c51471bc2
---
# Place custom ad markers on the timeline {#place-custom-ad-markers-on-the-timeline}

This example shows the recommended way to include custom ad markers on the playback timeline.

1. Translate the out-of-band ad-positioning information into a list/array of `RepaceTimeRange` class.
1. Create an instance of `CustomRangeMetadata` class, and use its `setTimeRangeList` method with the list/array as its argument to set its time range list.
1. Use its `setType` method to set the type to `MARK_RANGE`.
1. Use the `MediaPlayerItemConfig.setCustomRangeMetadata` method with the `CustomRangeMetadata` instance as its argument to set the custom range metadata.
1. Use the `MediaPlayer.replaceCurrentResource` method with the `MediaPlayerItemConfig` instance as its argument to set make the new resource the current one.
1. Wait for a `STATE_CHANGED` event, which reports that the player is in the `PREPARED` state.
1. Start video playback by calling `MediaPlayer.play`.

Here is the result of completing the tasks in this example: >
* If a `ReplaceTimeRange` overlaps another on the playback timeline, for example, the start position of a `ReplaceTimeRange` is earlier than an already placed end position, TVSDK silently adjusts the start of the offending `ReplaceTimeRange` to avoid the conflict. 

  This makes the adjusted `ReplaceTimeRange` shorter than originally specified. If the adjustment leads to a duration of zero, TVSDK silently drops the offending `ReplaceTimeRange`. 

* TVSDK looks for adjacent time ranges for custom ad breaks and clusters them into separate ad breaks. 

  Time ranges not adjacent to any other time range are translated into ad breaks that contain a single ad. 
* If the application tries to load a media resource whose configuration contains `CustomRangeMetadata` that can be used only in the context custom ad markers, TVSDK throws an exception if the underlying asset is not of type VOD. 
* When dealing with custom ad markers, TVSDK deactivates other ad-resolving mechanisms (for example, Adobe Primetime ad decisioning). 

  You can use any TVSDK ad-resolver module or the custom ad markers mechanism. When you use custom ad markers, the ad content is considered resolved and is placed on the timeline. 

The following code snippet places three time ranges on the timeline as custom ad-markers. 

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
