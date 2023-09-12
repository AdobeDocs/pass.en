---
description: Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.
title: Load a media resource in the MediaPlayer
exl-id: 2d5e95bc-3962-4356-b90f-e550066f7a70
---
# Load a media resource in the MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.

1. Set your MediaPlayer's playable item with the new resource to be played.

   Replace your existing MediaPlayer's currently playable item by calling `MediaPlayer.replaceCurrentItem` and passing an existing `MediaResource` instance. 

1. Register an implementation of the `MediaPlayer.PlaybackEventListener` interface with the `MediaPlayer` instance.

    * `onPrepared` 
    * `onStateChanged`, and check for INITIALIZED and ERROR.

1. When the state of the media player changes to INITIALIZED, you can call `MediaPlayer.prepareToPlay`

   The INITIALIZED state indicates that the media has been successfully loaded. Calling `prepareToPlay` starts the advertising resolution and placement process, if any.

1. When TVSDK calls the `onPrepared` callback, the media stream has successfully loaded and is prepared for playback.

   When the media stream is loaded, a `MediaPlayerItem` is created.

>If a failure occurs, the `MediaPlayer` switches to the ERROR status. It also notifies your application by calling your `PlaybackEventListener.onStateChanged`callback. 
>
>This passes several parameters:
>* A `state` parameter of type `MediaPlayer.PlayerState` with the value of `MediaPlayer.PlayerState.ERROR`. 
>
>* A `notification` parameter of type `MediaPlayerNotification` that contains diagnostic information about the error event. 

The following simplified sample code illustrates the process of loading a media resource: 

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 

```
