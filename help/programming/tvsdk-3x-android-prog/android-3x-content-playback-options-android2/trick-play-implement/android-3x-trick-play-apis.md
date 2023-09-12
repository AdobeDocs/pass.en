---
description: TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality that are related to fast forward and rewind.
title: Rate-change API elements
exl-id: 282d0d12-5244-4abd-893a-7e3c4d2f4fe8
---
# Rate-change API elements {#rate-change-api-elements}

TVSDK includes methods, properties, and events to determine valid rates, current rates, whether trick play is supported, and other functionality that are related to fast forward and rewind.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Use the following API elements to change play rates:

* `PlaybackRateEvent.getRate` 
* `MediaPlayerEvent.RATE_SELECTED` 
* `MediaPlayerEvent.RATE_PLAYING` 
* `MediaPlayerItem.isTrickPlaySupported` 
* `MediaPlayerItem.getAvailablePlaybackRates`, which specifies valid rates.

|  **Rate value**  | **Effect on playback**  |
|---|---|
|  2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0  | Switches to fast-forward mode with the specified multiplier faster than normal (for example, 4 is 4 times faster than normal)  |
|  -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0  | Switches to fast-rewind mode  |
|  1.0  | Switches to normal play mode (calling `play` is the same as setting the rate property to 1.0)  |
|  0.0  | Pauses (calling `pause` is the same as setting the rate property to 0.0)  |
