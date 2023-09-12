---
description: When you reset a MediaPlayer instance, it is returned to its uninitialized IDLE state as defined in MediaPlayerState.
title: Reset or reuse a MediaPlayer instance
exl-id: db8264f7-2f33-4441-86db-bb985edf7c3c
---
# Reset, reuse or remove a MediaPlayer instance {#reset-or-reuse-a-mediaplayer-instance}

You can reset, reuse, or release a MediaPlayer instance that you no longer need.

When you reset a MediaPlayer instance, it is returned to its uninitialized IDLE state as defined in MediaPlayerState.

This operation is useful in the following cases:

* You want to reuse a `MediaPlayer` instance but need to load a new `MediaResource` (video content) and replace the previous instance.

  Resetting allows you to reuse the `MediaPlayer` instance without the overhead of releasing resources, recreating the `MediaPlayer`, and reallocating resources. 

* When the `MediaPlayer` is in an ERROR state and needs to be cleared. 

  >[!IMPORTANT]
  >
  >This is the only way to recover from the ERROR state.

1. Call `reset` to return the `MediaPlayer` instance to its uninitialized state:

   ```java
   void reset() throws IllegalStateException; 
   
   ```

1. Use `MediaPlayer.replaceCurrentResource` to load another `MediaResource`.

   >[!TIP]
   >
   >To clear an error, load the same `MediaResource`.

1. When you receive the `STATUS_CHANGED` event callback with PREPARED status, start the playback.

## Release a MediaPlayer instance and resources{#release-a-mediaplayer-instance-and-resources}

You should release a MediaPlayer instance and resources when you no longer need the MediaResource.

When you release a `MediaPlayer` object, the underlying hardware resources that are associated with this `MediaPlayer` object are deallocated.

Here are some reasons to release a MediaPlayer:

* Holding unnecessary resources can affect performance. 
* Leaving an unnecessary `MediaPlayer` object can lead to continuous battery consumption for mobile devices. 
* If multiple instances of the same video-codec are not supported on a device, playback failure might occur for other applications.

1. Release the `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

After the `MediaPlayer` instance is released, you can no longer use it. If any method of the `MediaPlayer` interface is called after it is released, an `IllegalStateException` is thrown.
