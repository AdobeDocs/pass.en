---
title: Limitations and behavior for trick play
description: Limitations and behavior for trick play
copied-description: yes
exl-id: 5acd91e6-6022-4365-be2b-e84f0a0a91d1
---
# Limitations and behavior for trick play {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitations for trick play mode:

* The master playlist must contain Iframe-only segments.

  Only the key frames from the Iframe track are displayed on the screen. 
* The audio track and closed captions are disabled. 
* Play and pause are enabled. 
* You can exit trick-play mode into any allowed playback rate (play or pause). 
* When ads are incorporated in the stream:

    * You can go to trick play only while playing the main content. An error is dispatched if you try to switch to trick play during an ad break. 
    * After starting trick play mode, ad breaks are ignored and no ad events are fired. 
    * The timeline exposed by TVSDK to the player is not modified even if ad breaks are skipped. 
    * The current time value jumps forward (on fast forward) or backward (on fast rewind) with the duration of the skipped ad break.

      This jump behavior for the current time allows the stream duration to remain unmodified during trick play. Your player can track the time relative only to the main content. No time jumps are performed on the values returned for the local time when skipping an ad. 
    * The `MediaPlayerEvent.AD_BREAK_SKIPPED` event is dispatched immediately before an ad break is about to be skipped.

      Your player can use this event to implement custom logic related to the skipped ad breaks. 
    
    * Exiting trick play invokes the same ad playback policy as when exiting seek.

      As with seeking, the behavior depends on whether your application's playback policy is different from the default. The default is that the last skipped ad break is played at the point where you come out of trick play.
