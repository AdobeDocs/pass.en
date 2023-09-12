---
description: Load a resource by directly instantiating a MediaResource and loading the video content to be played.
title: Load a media resource in the MediaPlayer
exl-id: b775c33e-399c-4a03-a132-407944f07706
---
# Load a media resource in the MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Load a resource by directly instantiating a MediaResource and loading the video content to be played.

1. Set your `MediaPlayer` object's playable item with the new resource to be played.

   Replace your existing `MediaPlayer` object's currently playable item by calling `replaceCurrentResource` and passing an existing `MediaResource` instance. 

1. Wait for Browser TVSDK to dispatch `AdobePSDK.MediaPlayerStatusChangeEvent` with `event.status` that is equal to any of the following:

    * `MediaPlayerStatus.INITIALIZED` 
    * `MediaPlayerStatus.PREPARED` 
    * `MediaPlayerStatus.ERROR`

       Through these events, the MediaPlayer object notifies your application whether the media resource is successfully loaded. 
    
1. When the state of the media player changes to `MediaPlayerStatus.INITIALIZED`, you can call `MediaPlayer.prepareToPlay`.

   The INITIALIZED state indicates that the media has been successfully loaded. Calling `prepareToPlay` starts the advertising resolution and placement process, if any.
1. When Browser TVSDK dispatches the `MediaPlayerStatus.PREPARED` event the media stream has successfully loaded (a MediaPlayerItem is created) and is prepared for playback.

If a failure occurs, the `MediaPlayer` switches to the `MediaPlayerStatus.ERROR`. 

It also notifies your application by dispatching the `MediaPlayerStatus.ERROR` event.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

The following simplified sample code illustrates the process of loading a media resource: 

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
