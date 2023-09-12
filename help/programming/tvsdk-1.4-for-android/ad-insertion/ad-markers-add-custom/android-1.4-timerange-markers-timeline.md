---
description: This example shows the recommended way to include TimeRange specifications on the playback timeline.
title: Place TimeRange ad markers on the timeline
exl-id: 53b48d5b-7725-48ae-848a-ccd2a54b132a
---
# Place TimeRange ad markers on the timeline {#place-timerange-ad-markers-on-the-timeline}

This example shows the recommended way to include TimeRange specifications on the playback timeline.

1. Translate the out-of-band ad-positioning information into a list of `TimeRange` specifications (that is, instances of the `TimeRange` class).
1. Use the set of `TimeRange` specifications to populate an instance of the `TimeRangeCollection` class.
1. Pass the Metadata instance, which can be obtained from the `TimeRangeCollection` instance, to the `replaceCurrentItem` method (part of the MediaPlayer interface).
1. Wait for TVSDK to transition to the `PREPARED` state by waiting for the `PlaybackEventListener#onPrepared` callback to be triggered.
1. Start video playback by calling the `play()` method (part of the `MediaPlayer` interface).

* Handling timeline conflicts: There might be cases when some `TimeRange` specifications overlap on the playback timeline. For example, the value of the start position corresponding to a `TimeRange` specification might be lower than the value of the end position that was already placed. In this case, TVSDK silently adjusts the start position of the offending `TimeRange` specification to avoid timeline conflicts. Through this adjustment, the new `TimeRange` becomes shorter than originally specified. If the adjustment is so extreme that it would lead to a `TimeRange` with a duration of zero ms, TVSDK silently drops the offending `TimeRange` specification. 
* When `TimeRange` specifications for custom ad breaks are provided, TVSDK attempts to translate these into ads that are grouped inside ad breaks. TVSDK looks for adjacent `TimeRange` specifications and clusters them into separate ad breaks. If there are time ranges that are not adjacent to any other time range, they are translated into ad breaks that contain a single ad. 
* It is assumed that the media player item that is being loaded points to a VOD asset. TVSDK checks this whenever your application tries to load a media resource whose metadata contains `TimeRange` specifications that can be used only in the context of the custom ad-markers feature. If the underlying asset is not of type VOD, TVSDK library throws an exception. 
* When dealing with custom ad markers, TVSDK deactivates other ad-resolving mechanisms (via Adobe Primetime ad decisioning (previously known as Auditude) or other ad provisioning system). You can use either one of the various ad-resolver modules provided by TVSDK or the custom ad-markers mechanism. When using the custom ad-markers API, the ad content is considered already resolved and placed on the timeline. 

The following code snippet provides a simple example where a set of three TimeRange specifications are placed on the timeline as custom ad-markers. 

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 

```
