---
description: When your playback includes advertising, Browser TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.
title: Order of advertising events
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
---
# Order of advertising events{#order-of-advertising-events}

When your playback includes advertising, Browser TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

When playing ads, the order of events is:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED` 
* The following are dispatched for every ad in the ad break:

    * `AdobePSDK.PSDKEventType.AD_STARTED` 
    * `AdobePSDK.PSDKEventType.AD_PROGRESS` (multiple times during an ad's playback) 
    * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

The following example shows a typical progression of ad playback events:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
