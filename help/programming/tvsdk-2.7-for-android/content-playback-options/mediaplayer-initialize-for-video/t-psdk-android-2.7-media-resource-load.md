---
description: Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.
title: Load a media resource in the media player
exl-id: ee11876b-c752-46cc-8e65-8c1608a41362
---
# Load a media resource in the media player {#load-a-media-resource-in-the-media-player}

Load a resource by directly instantiating a MediaResource and loading the video content to be played. This is one way of loading a media resource.

1. Set the media player to play the new resource.

   Replace the currently playable item by calling `MediaPlayer.replaceCurrentResource()` and passing an existing `MediaResource` instance.

   This starts the resource loading process. 

1. Register the `MediaPlayerEvent.STATUS_CHANGED` event with the `MediaPlayer` instance. In the callback, check for at least the following status values:

    * `MediaPlayerStatus.PREPARED` 
    * `MediaPlayerStatus.INITIALIZED` 
    * `MediaPlayerStatus.ERROR`

   Through these events, the `MediaPlayer` object notifies your application when it has successfully loaded the media resource.
1. When the status of the media player changes to `INITIALIZED`, you can call `MediaPlayer.prepareToPlay()`.

   This status indicates that the media has been successfully loaded. The new `MediaPlayerItem` is ready for playback. Calling `prepareToPlay()` starts the advertising resolution and placement process, if any.

If a failure occurs, the media player switches to the `ERROR` status. 

The following simplified sample code illustrates the process of loading a media resource: 

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 

```
