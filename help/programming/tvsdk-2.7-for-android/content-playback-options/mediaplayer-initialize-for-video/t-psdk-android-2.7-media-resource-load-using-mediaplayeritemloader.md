---
description: Using MediaPlayerItemLoader helps you obtain information about a media stream without instantiating a MediaPlayer instance. This is especially useful in pre-buffering streams so that playback can begin without delay.
title: Load a media resource using MediaPlayerItemLoader
exl-id: 6bd081bb-b92b-4c0a-a3bc-ef2128d0d8bf
---
# Load a media resource using MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Using MediaPlayerItemLoader helps you obtain information about a media stream without instantiating a MediaPlayer instance. This is especially useful in pre-buffering streams so that playback can begin without delay.

The `MediaPlayerItemLoader` class helps you exchange a media resource for the current `MediaPlayerItem` without attaching a view to a `MediaPlayer` instance, which would allocate video decoding hardware resources. Additional steps are necessary for DRM-protected content, but this manual does not describe them.

>[!IMPORTANT]
>
>TVSDK does not support a single `QoSProvider` to work with both `itemLoader` and `MediaPlayer`. If your application uses Instant On, the application needs to maintain two `QoS` instances and manage both instances for the information. See  [instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) for more information.

1. Create an instance of `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
    
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
    
           public void onBufferingBegin() { 
               //Do something 
           } 
    
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
    
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   
   ```

   >[!TIP]
   >
   >Create a separate instance of `MediaPlayerItemLoader` for each resource. Do not use one `MediaPlayerItemLoader` instance to load multiple resources.

1. Implement the `ItemLoaderListener` class to receive notifications from the `MediaPlayerItemLoader` instance.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
     
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   In the `onLoadComplete()` callback, do one of the following:

    * Ensure that anything that might affect buffering, for example, selecting WebVTT or audio tracks, is complete and call `prepareBuffer()` to take advantage of instant on. 
    * Attach the item to the `MediaPlayer` instance by using `replaceCurrentItem()`.

    If you call `prepareBuffer()`, you receive the BUFFER_PREPARED event in your `onBufferPrepared` handler when the preparation is finished. 

1. Call `load` on the `MediaPlayerItemLoader` instance and pass the resource to be loaded, and optionally the content ID, and a `MediaPlayerItemConfig` instance.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. To buffer from a point other than the beginning of the stream, call `prepareBuffer()` with the position (in milliseconds) at which to start buffering.
1. Use the `replaceCurrentItem()` and `play()` methods of `MediaPlayer` to start playing from that point.
1. Wait for idle status and call `replaceCurrentItem`.
1. Play the item.

    * If the item is loaded but not buffered:

        1. Wait for initialized status. 
        1. Call `prepareToPlay()`. 
        1. Wait for the PREPARED status. 
        1. Call `play()`.

    * If the item is buffered:

        1. Wait for the buffer prepared event. 
        1. Call `play()`.
