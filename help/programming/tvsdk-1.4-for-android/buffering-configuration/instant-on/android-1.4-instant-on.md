---
description: The term instant on refers to preloading one or more channels so that a user selecting a channel or switching channels sees content playing immediately. The buffering is already done by the time the user starts watching.
title: Instant on
exl-id: f640f208-d1b3-467a-be97-38690e10b7ed
---
# Instant on {#instant-on}

The term instant on refers to preloading one or more channels so that a user selecting a channel or switching channels sees content playing immediately. The buffering is already done by the time the user starts watching.

 Without instant on, TVSDK initializes the media to be played but does not start buffering the stream until the application calls `play`. The user sees no content until buffering is complete. With instant on, you can launch multiple media player (or media-player item loader) instances, and TVSDK starts buffering the streams immediately.

When a user changes the channel and the stream has buffered properly, calling `play` on the new channel starts playback immediately.

Although there are no limits to the number of `MediaPlayer` instances that TVSDK can run, running more instances consumes more resources. Application performance can be affected by the number of instances running. For more information about these instances, see [Load a media resource using MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configure buffering for instant-on playback {#configure-buffering-for-instant-on-playback}

With instant on, users can switch channels and the playback starts immediately without waiting time. When you enable instant on, TVSDK buffers one or more channels before playback begins.

1. Confirm that the resource has loaded and is ready for playing by verifying that the state is PREPARED.
1. Before calling `play`, call `prepareBuffer` for each `MediaPlayer` instance.

   This enables instant on, which means that TVSDK starts buffering without actually playing the media resource. TVSDK dispatches the `BUFFERING_COMPLETED` event when the buffer is full.

   >[!NOTE]
   >
   >By default, `prepareBuffer` and `prepareToPlay` set up the media stream to start playing from the beginning. To start at another position, pass the position (in milliseconds) into `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. When you receive the `BUFFERING_COMPLETE` event, start playing the item or display visual feedback to indicate that the content is completely buffered.

   If you call `play`, playback should begin immediately. 

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
