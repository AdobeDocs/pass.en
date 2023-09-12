---
description: Enabling instant on means that one or more channels are preloaded. When users select a channel or switch channels, the content plays immediately. The buffering is complete by the time the user starts watching.
title: Instant On
exl-id: a9c0b9d0-ef2b-4113-bd08-e2b2792b04fb
---
# Instant On {#instant-on}

Enabling instant on means that one or more channels are preloaded. When users select a channel or switch channels, the content plays immediately. The buffering is complete by the time the user starts watching.

Without Instant On, TVSDK initializes the media to be played but does not start buffering the stream until the application calls `play`. The user sees no content until buffering is complete. With Instant On, you can launch multiple media player (or media-player item loader) instances, and TVSDK starts buffering the streams immediately. When a user changes the channel and the stream has buffered properly, calling `play` on the new channel starts playback immediately.

Although there are no limits to the number of `MediaPlayer` and `MediaPlayerItemLoader` instances that TVSDK can run, running more instances consumes more resources. Application performance can be affected by the number of instances that are running. For more information about `MediaPlayerItemLoader`, see [Load a media resource in the media player](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK does not support a single `QoSProvider` to work with both `itemLoader` and `MediaPlayer`. If the customer uses Instant On, the application needs to maintain two QoS instances and manage both instances for the information.

For more information about `MediaPlayerItemLoader`, see [Load a media resource using MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## Add a QoS Provider instance to mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Create and attach a QoS Provider to a `mediaPlayerItemLoader` instance 

  ```
  // Create an instance of QoSProvider  
  private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
  // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
  // (before calling load API on mediaPlayerItemLoader instance)  
  _qosProvider.attachMediaPlayerItemLoader(this._loader); 
  ```

  Once the playback starts, use the `_qosProvider` to get `timeToLoad` and `timeToPrepare` QoSdata. The remaining QoS metrics can be retrieved by using the `QoSProvider` attached to the `mediaPlayer`.

  For more information about `MediaPlayerItemLoader`, see [Load a media resource using MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## Configure buffering for Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK provides methods and statuses to allow you use Instant On with a media resource.

>[!NOTE]
>
>Adobe recommends using `MediaPlayerItemLoader` for InstantOn. To use `MediaPlayerItemLoader`, rather than `MediaPlayer`, see  media-resource-load-using-mediaplayeritemloader .

1. Confirm that the resource has loaded, and the player is prepared to play the resource. 
1. Before calling `play`, call `prepareBuffer` for each `MediaPlayer` instance. 

   >[!NOTE]
   >
   >`prepareBuffer` enables Instant On, and TVSDK starts buffering immediately and dispatches the `BUFFERING_COMPLETED` event when the buffer is full.

   >[!TIP]
   >
   >By default, `prepareBuffer` and `prepareToPlay` set up the media stream to start playing from the beginning. To start at another position, pass the position (in milliseconds) to `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. When you receive the `BUFFERING_COMPLETE` event, start playing the item or display visual feedback to indicate that the content is completely buffered. 

   >[!NOTE]
   >
   >If you call `play`, playback should begin immediately.
