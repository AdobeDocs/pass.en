---
description: You can configure visuals to notify the user that content is buffering.
title: Buffering
exl-id: 1b2f32b4-1839-4256-82d6-b262569aa751
---
# Buffering{#buffering}

You can configure visuals to notify the user that content is buffering.

Listen for `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` and `AdobePSDK.PSDKEventType.BUFFERING_END` events. For example: 

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

The UI Framework provides default buffering overlay behavior implementation, which can be extended as shown below: 

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 

```

Here is what the result DOM looks like: 

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 

```
