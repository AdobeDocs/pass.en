---
description: You can reset, reuse, or release a MediaPlayer instance that you no longer need.
title: Reuse or remove a MediaPlayer instance
exl-id: 8b84c7f1-713a-46b4-8eb7-d699a79e74b7
---
# Reuse or remove a MediaPlayer instance {#reuse-or-remove-a-mediaplayer-instance}

You can reset, reuse, or release a MediaPlayer instance that you no longer need.

## Reset or reuse a MediaPlayer instance {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

When you reset a `MediaPlayer` instance, it is returned to its uninitialized IDLE status as defined in `MediaPlayerStatus`.

This operation is useful in the following cases:

* You want to reuse a `MediaPlayer` instance but need to load a new `MediaResource` (video content) and replace the previous instance.

  Resetting allows you to reuse the `MediaPlayer` instance without the overhead of releasing resources, recreating the `MediaPlayer`, and reallocating resources. 

* When the `MediaPlayer` is in ERROR status and needs to be cleared. 

  >[!IMPORTANT]
  >
  >This is the only way to recover from the ERROR status.

    1. Call `reset` to return the `MediaPlayer` instance to its uninitialized status:     
    
       ```java    
       void reset() throws MediaPlayerException; 
       
       ```

    1. Use `MediaPlayer.replaceCurrentResource()` to load another `MediaResource`.     
    
       >[!NOTE]
       >
       >To clear an error, load the same `MediaResource`.

    1. When you receive the `STATUS_CHANGED` event callback with `PREPARED` status, start the playback.

## Release a MediaPlayer instance and resources {#section_13A0914AFF784943ABC343F7EB249C4E}

You should release a `MediaPlayer` instance and resources when you no longer need the `MediaResource`.

When you release a `MediaPlayer` object, the underlying hardware resources that are associated with this `MediaPlayer` object are deallocated.

Here are some reasons to release a `MediaPlayer`:

* Holding unnecessary resources can affect performance. 
* Leaving an unnecessary `MediaPlayer` object instantiated can lead to continuous battery consumption for mobile devices. 
* If multiple instance
s of the same video-codec are not supported on a device, playback failure might occur for other applications.

* Release the `MediaPlayer`. 

  ```java
  void release() throws MediaPlayerException;
  ```

  >[!NOTE]
  >
  >After the `MediaPlayer` instance is released, you can no longer use it. If any method of the `MediaPlayer` interface is called after it is released, a `MediaPlayerException` is thrown.
