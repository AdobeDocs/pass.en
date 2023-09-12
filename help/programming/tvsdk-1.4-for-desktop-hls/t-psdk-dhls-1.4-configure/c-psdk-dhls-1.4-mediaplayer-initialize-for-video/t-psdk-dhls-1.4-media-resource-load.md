---
description: Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.
title: Load a media resource in the MediaPlayer
exl-id: 8258c45e-f8bf-434d-9621-88c189e1530d
---
# Load a media resource in the MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.

1. Set your `MediaPlayer` object's playable item with the new resource to be played.

   Replace your existing MediaPlayer's currently playable item by calling `MediaPlayer.replaceCurrentResource` and passing an existing `MediaResource` instance. 

1. Check for at least the following changes:

    * INITIALIZED 
    * PREPARED 
    * ERROR

       Through these events, the `MediaPlayer` object can notify your application when the media resource is successfully loaded. 
    
1. When the state of the media player changes to INITIALIZED, you can call `MediaPlayer.prepareToPlay`

   The INITIALIZED state indicates that the media has been successfully loaded. Calling `prepareToPlay` starts the advertising resolution and placement process, if any.

1. When the media player status changes to PREPARED, the media stream has successfully loaded and is prepared for playback.

   When the media stream is loaded, a `MediaPlayerItem` is created.

If a failure occurs, the MediaPlayer switches to the ERROR status. It also notifies your application by dispatching the `STATUS_CHANGED` event to your `MediaPlayerStatusChangeEvent` callback. 

This passes several parameters:
* A `type` parameter of type string with the value `ERROR`. 

* A `MediaError` parameter that you can use to get a notification that contains diagnostic information about the error event. 


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

The following simplified sample code illustrates the process of loading a media resource: 

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
