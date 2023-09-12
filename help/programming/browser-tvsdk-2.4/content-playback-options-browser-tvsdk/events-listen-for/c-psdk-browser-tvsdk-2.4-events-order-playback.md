---
description: Browser TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.
title: Order of playback events
exl-id: fd9dc0d5-0f39-4a6d-9d88-1fd49946fedf
---
# Order of playback events{#order-of-playback-events}

Browser TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

The following examples show the order of some events that include playback events.

* When successfully loading a media resource through `replaceCurrentResource`, the order of events is:

    * `AdobePSDK.MediaPlayerStatusChangeEvent` with `event.status =`

        * `MediaPlayerStatus.INITIALIZING` 
        * `MediaPlayerStatus.INITIALIZED`

* When preparing for playback through `MediaPlayer.prepareToPlay`, the order of events is:

    * `AdobePSDK.MediaPlayerStatusChangeEvent` with `event.status =`

        * `MediaPlayerStatus.PREPARING` 
        * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

The following example shows a typical progression of events:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```
