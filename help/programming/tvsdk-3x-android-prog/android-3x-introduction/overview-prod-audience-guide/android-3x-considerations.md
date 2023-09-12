---
description: To use TVSDK most effectively, you should consider certain details of its operation and follow certain best practices.
title: Considerations and best practices
exl-id: c53b3e13-246b-4224-9751-0bc88fad12ed
---
# Considerations and best practices {#considerations-and-best-practices}

To use TVSDK most effectively, you should consider certain details of its operation and follow certain best practices.

## Considerations {#section_tvsdk_considerations}

Remember the following information when using TVSDK:

* The TVSDK API is implemented in Java.
* Adobe Primetime does not currently work on Android emulators.

  You must use real devices for testing.
* Playback is supported only for HTTP Live Streaming (HLS) content. 
* Main video content can be multiplexed (video and audio streams in the same rendition) or nonmultiplexed (video and audio streams in separate renditions). 
* Currently, you need to run most TVSDK API operations on the UI thread, which is the main Android thread.

  Operations that run correctly on the main thread may throw an error and exit when run on a background thread. 
* Video playback requires the Adobe Video Engine (AVE). This affects how and when media resources can be accessed:

    * Closed captioning is supported to the extent provided by the AVE. 
    * Depending on encoder precision, the actual encoded media duration might differ from the durations that are recorded in the stream resource manifest.

      There is no reliable way to resynchronize between the ideal virtual timeline and the actual playout timeline. Progress tracking of the stream playback for ad management and Video Analytics must use the actual playout time, so reporting and user interface behavior might not precisely track the media and advertisement content. 
    * The incoming user agent name for all media requests from the TVSDK on this platform is assigned the following string pattern:     
    
      ```    
      "Adobe Primetime/" + originalUserAgent
      ```    
    
      All ad-related calls use the Android default user agent or the custom user agent if you set it while setting up ad-insertion metadata.

## Best practices {#section_tvsdk_best_practices}

Here are recommended practices for TVSDK:

* Use HLS version 3.0 or above for program content. 
* Run most TVSDK operations on the main (UI) thread, not on background threads. 
* For TVSDK 3.0 for Android, lazy ad resolving is on by default.

For content with no pre-roll or mid-roll, you can use `AdvertisingMetadata.setPreroll(false)` to accelerate content loading.
