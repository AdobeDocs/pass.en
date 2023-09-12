---
description: When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.
title: Implement fast forward and rewind
exl-id: 21f9a3f6-1cae-4240-991d-c03a0e49adf3
---
# Implement fast forward and rewind{#implement-fast-forward-and-rewind}

When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.

>[!IMPORTANT]
>
>* Trick play mode is supported only for MPEG Dash and HLS VOD content. 
>* Trick play mode is not supported for live streams or ads. 
>* When switching from main content to an ad, Browser TVSDK leaves trick play mode. 
>

To switch the speed, you must set one value. 

1. Move from normal play mode (1x) to trick play mode by setting the rate on the `MediaPlayer` to an allowed value.

    * The `MediaPlayerItem` class defines the allowed playback rates. 
    * Browser TVSDK selects the closest allowed rate if the specified rate is not allowed.

       The following example function sets the rate:     
    
       ```js    
       setTrickPlayRate = function (player, trickPlayRate) { 
                     player.rate = trickPlayRate; 
       }
       ```

       The following example function can be used to query the available playback rates:     
    
       ```js    
       getAvailableTrickPlayRates = function (player) { 
                var item = player.currentItem; 
                var availableRates = item. availablePlaybackRates; 
                return availableRates; 
       } 
       
       ```

1. You can optionally listen for rate-change events, which let you know when you requested a rate change and when a rate change actually happens.

       Browser TVSDK dispatches the following events related to trick play:

    * `AdobePSDK.PSDKEventType.RATE_SELECTED` when the `rate` value changes to a different value. 
    
    * `AdobePSDK.PSDKEventType.RATE_PLAYING` when playback resumes at the selected rate.

       Browser TVSDK dispatches both of these events when the player returns from trick-play mode to normal play mode.

## Rate-change API elements {#rate-change-API-elements}

Browser TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality related to fast forward and rewind.

Use the following API elements to change play rates:

* `MediaPlayer.rate` 
* `PlaybackRateEvent.rate` 
* `MediaPlayerItem.istrickPlaySupported` 
* `MediaPlayerItem.availablePlaybackRates` - specifies valid rates.

  |  Rate value  | Effect on playback  |
  |---|---|
  |  2.0, 4.0, 8.0, 16.0, 32.0, 64.0  | Switches to fast-forward mode with the specified multiplier faster than normal (for example, 4 is 4 times faster than normal)  |
  |  -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  | Switches to fast-rewind mode  |
  |  1.0  | Switches to normal play mode (calling `play` is the same as setting the rate property to 1.0)  |
  |  0.0  | Pauses (calling `pause` is the same as setting the rate property to 0.0)  |

## Limitations and behavior for trick-play {#limitations-and-behavior-trick-play}

There are some limitations and some issues in the way trick play mode behaves. 

Here is a list of the trick-play mode limitations:

* If the stream does not contain a trick play adaptation, fast rewind is disabled, and maximum play rate for fast forward is limited to 8. 
* When trick play adaptations are used to provide the trick mode, the audio track is disabled. 
* In trick play mode, the switching of audio and closed captions tracks is disabled. 
* Play and pause are enabled. 
* On seek, if playback is in trick play mode, playback rate is set to 1 and normal playback resumes. 
* The adaptive bit rate (ABR) logic is enabled.

  When using normal adaptations the profiles are restricted between `ABRControlParameters.minBitRate` and `ABRControlParameters.maxBitRate`. When using trick play adaptations, the profiles are restricted between `ABRControlParameters.minTrickPlayBitRate` and `ABRControlParameters.maxTrickPlayBitRate`.
