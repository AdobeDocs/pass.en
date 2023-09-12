---
description: When your playback includes advertising, TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.
title: Order of advertising events
exl-id: 131b1dc1-3a59-4276-b639-d004ab7394ea
---
# Order of advertising events{#order-of-advertising-events}

When your playback includes advertising, TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

When playing ads, the order of events is:

* `AdBreakPlaybackEvent.AD_BREAK_STARTED` 
* The following are dispatched for every ad in the ad break:

    * `AdPlaybackEvent.AD_STARTED` 
    * `AdPlaybackEvent.AD_PROGRESS` (multiple times during an ad's playback) 
    * `AdClickEvent.AD_CLICK` (for each click) 
    * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

The following example shows a typical progression of ad playback events:

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 

```
