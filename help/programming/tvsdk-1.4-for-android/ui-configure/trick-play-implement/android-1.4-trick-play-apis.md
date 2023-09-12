---
description: TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality related to fast forward and rewind.
title: Rate-change API elements
exl-id: 9c366645-5ce5-485c-8423-cb0ed4bd2677
---
# Rate-change API elements{#rate-change-api-elements}

TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality related to fast forward and rewind.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Use the following API elements to change play rates:

* `PlaybackRateEvent.getRate` 
* `MediaPlayer.getLocalTime` 
* `MediaPlayerEvent.RATE_SELECTED` 
* `MediaPlayerEvent.RATE_PLAYING` 
* `MediaPlayerItem.istrickPlaySupported` 
* `MediaPlayerEvent.AD_BREAK_SKIPPED` 
* `MediaPlayerItem.getAvailablePlaybackRates` - specifies valid rates.

|  Rate value  | Effect on playback  |
|---|---|
|  2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0  | Switches to fast-forward mode with the specified multiplier faster than normal (for example, 4 is 4 times faster than normal)  |
|  -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0  | Switches to fast-rewind mode  |
|  1.0  | Switches to normal play mode (calling `play` is the same as setting the rate property to 1.0)  |
|  0.0  | Pauses (calling `pause` is the same as setting the rate property to 0.0)  |
