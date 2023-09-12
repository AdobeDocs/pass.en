---
description: When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.
title: Implement fast forward and rewind
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
---
# Implement fast forward and rewind {#implement-fast-forward-and-rewind}

When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.

To switch the speed, you must set one value. 

1. Move from normal play mode (1x) to trick play mode by setting the `rate` property on the `MediaPlayer` to an allowed value.

    * The `MediaPlayerItem` class defines the allowed playback rates. 
    * TVSDK selects the closest allowed rate if the specified rate is not allowed.

       When the trickplay rate is changed from 0 (pause) or 1 (normal play) to a rate that is greater than 1 or less than -1, all the ads on the timeline are removed. There is only one period on the entire timeline that facilitates a trickplay action to allow the content to be fast forwarded and rewound without stopping at any ad position. This action is enabled by a timeline detachment action on TVSDK to remove all the resolved adBreaks. When trickplay resumes at 0 or 1, the adBreaks are first restored by the timeline attachment action.

       Remember the following information:

    * If the trickplay action is to rewind the content, the playback resumes when rate is changed to 1. 
    * If the trickplay action is to fast forward the content, the last skipped adBreak plays at the resume position.

   This example sets the player's internal playback rate to the requested rate.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
    
       _player.rate = newRate; 
   } 
   
   ```

1. You can optionally listen for rate-change events, which let you know when you requested a rate change and when a rate change actually happens.

    TVSDK dispatches the following events related to trick play:

    * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` when the `rate` value changes to a different value. 
    
    * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` when playback resumes at the selected rate.

    TVSDK dispatches both of these events when the player returns from trick-play mode to normal play mode.

## Rate-change API elements {#rate-change-api}

TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality related to fast forward and rewind.

Use the following API elements to change play rates:

* `MediaPlayer.rate` property with setter and getter functions 
* `MediaPlayer.localTime property` with getter function 
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED` 
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING` 
* `MediaPlayerItem.IsTrickPlaySupported` property with getter function 
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` 
* `MediaPlayerItem.availablePlaybackRates` property with getter function - specifies valid rates.

|  Rate value  | Effect on playback  |
|---|---|
|  2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0   | Switches to fast-forward mode with the specified multiplier faster than normal (for example, 4 is 4 times faster than normal)  |
|  -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0   | Switches to fast-rewind mode  |
|  1.0  | Switches to normal play mode (calling `play` is the same as setting the rate property to 1.0)  |
|  0.0  | Pauses (calling `pause` is the same as setting the rate property to 0.0)  |

## Limitations and behavior for trick play {#limitations-behavior-trick-play}

Here are the limitations for trick play mode:

* The master playlist must contain I-frame-only segments. Only the key frames from the I-frame track are displayed on the screen. 
* The audio track and closed captions are disabled. 
* Adaptive bit rate (ABR) logic is disabled. TVSDK selects one bit rate between the lowest provided rate and 800 kbps and uses that rate during the entire trick-play session. 
* Play and pause are enabled. 
* Seek is disallowed. To seek, call `pause` to exit trick play mode and then call `seek`. 

* You can exit trick-play mode into any allowed playback rate (play or pause). 
* When ads are incorporated in the stream:

    * You can go to trick play only while playing the main content. An error is dispatched if you try to switch to trick play during an ad break. 
    * After commencing trick play mode, ad breaks are ignored and no ad events are fired. 
    * The timeline exposed by TVSDK to the player application is not modified even if ad breaks are skipped. 
    * The `MediaPlayer.currentTime` property jumps forward (on fast forward) or backward (on fast rewind) with the duration of the skipped ad break. This jump behavior for the current time allows the stream duration to remain unmodified during trick play. Your player application can use the `localTime` property to track the time relative only to the main content. No time jumps are performed on the values returned for the local time when skipping an ad. 
    
    * The `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` event is dispatched immediately before an ad break is about to be skipped. Your player can use this event to implement custom logic related to the skipped ad breaks. 
    * Exiting trick play invokes the same ad playback policy as when exiting seek.

      Therefore, as in seeking, the behavior depends on whether your application's playback policy is different from the default. The default is that the last skipped ad break is played at the point where you come out of trick play.
