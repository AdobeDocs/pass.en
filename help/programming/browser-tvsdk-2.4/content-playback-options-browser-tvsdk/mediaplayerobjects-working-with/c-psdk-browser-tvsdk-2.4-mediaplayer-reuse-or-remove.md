---
description: You can reset, reuse, or release a MediaPlayer instance that you no longer need.
title: Reuse or remove a MediaPlayer instance
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
---
# Reuse or remove a MediaPlayer instance{#reuse-or-remove-a-mediaplayer-instance}

You can reset, reuse, or release a MediaPlayer instance that you no longer need.

## Reset or reuse a MediaPlayer instance {#section_C183E6164C184C3CBC5321FC6A2528EA}

You can reset a `MediaPlayer` instance to return it to its uninitialized IDLE state as defined in `MediaPlayerStatus`. You can also replace the current media item or set a new one using a previously loaded media resource.

This operation is useful in the following cases:

* You want to reuse a `MediaPlayer` instance but need to load a new `MediaResource` (video content) and replace the previous instance.

  Resetting allows you to reuse the `MediaPlayer` instance without the overhead of releasing resources, recreating the `MediaPlayer`, and reallocating resources. The `replaceCurrentItem` method automatically does these steps for you. 

* When the `MediaPlayer` is in an ERROR state and needs to be cleared. 

  >[!IMPORTANT]
  >
  >This is the only way to recover from the ERROR state.

1. Call `MediaPlayer.reset()` to return the `MediaPlayer` instance to its uninitialized state: 

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Call `MediaPlayer.replaceCurrentItem()` to load another `MediaResource` 

   >[!TIP]
   >
   >To clear an error, load the same `MediaResource`.

1. Call the `prepareToPlay()` method. 

   >[!NOTE]
   >
   >When you receive the `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` event with the PREPARED state, you can start the playback.

## Release a MediaPlayer instance and resources {#section_2D159975C82245098E7078FE0B1578CE}

You should release a `MediaPlayer` instance and resources when you no longer need the MediaResource.

Here are some reasons to release a `MediaPlayer`:

* Holding unnecessary resources can affect performance. 
* Leaving an unnecessary `MediaPlayer` object can lead to continuous battery consumption for mobile devices. 
* If multiple instances of the same video-codec are not supported on a device, playback failure might occur for other applications.

* Release the `MediaPlayer`. 

  ```js
  void release()
  ```

  >[!NOTE]
  >
  >After the `MediaPlayer` instance is released, you can no longer use it. If any method of the `MediaPlayer` interface is called after it is released, an `IllegalStateException` is thrown.
