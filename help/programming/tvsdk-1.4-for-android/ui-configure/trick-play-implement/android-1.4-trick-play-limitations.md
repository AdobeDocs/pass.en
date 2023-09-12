---
description: There are some limitations and some issues in the way trick play mode behaves.
title: Limitations and behavior for trick play
exl-id: 98558970-9e5e-4dc1-a327-63d9db1d4fed
---
# Limitations and behavior for trick play{#limitations-and-behavior-for-trick-play}

There are some limitations and some issues in the way trick play mode behaves.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Here are the limitations for trick play mode:

* The master playlist must contain I-frame-only segments. Only the key frames from the I-frame track are displayed on the screen. 
* The audio track and closed captions are disabled. 
* Adaptive bit rate (ABR) logic is disabled. TVSDK selects one bit rate between the lowest provided rate and 800 kbps and uses that rate during the entire trick-play session. 
* Play and pause are enabled. 
* Seek is disallowed. To seek, call `pause` to exit trick play mode and then call `seek`. 

* You can go from trick play mode into any allowed playback rate (play or pause). 
* When ads are incorporated in the stream:

    * You can go to trick play only while playing the main content. An error is dispatched if you try to switch to trick play during an ad break. 
    * After commencing trick play mode, ad breaks are ignored and no ad events are fired. 
    * The timeline exposed by TVSDK to the player application is not modified even if ad breaks are skipped. 
    * The current time value jumps forward (on fast forward) or backward (on fast rewind) with the duration of the skipped ad break. This jump behavior for the current time allows the stream duration to remain unmodified during trick play. Your player application can  get the local time value to track the time relative only to the main content. No time jumps are performed on the values returned for the local time when skipping an ad. 
    * The `MediaPlayerEvent.AD_BREAK_SKIPPED` event is dispatched immediately before an ad break is about to be skipped. Your player can use this event to implement custom logic related to the skipped ad breaks. 
    * Exiting trick play invokes the same ad playback policy as when exiting seek.

      Therefore, as in seeking, the behavior depends on whether your application's playback policy is different from the default. The default is that the last skipped ad break is played at the point where you come out of trick play mode.
