---
description: By default, when starting playback, VOD media starts at 0 (MediaPlayer.LIVE_POINT). You can override the default behavior.
title: Enter a stream at a specific time
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
---
# Enter a stream at a specific time {#enter-a-stream-at-a-specific-time}

By default, when starting playback, VOD media starts at 0 (MediaPlayer.LIVE_POINT). You can override the default behavior.

1. Pass a position to `MediaPlayer.prepareToPlay`.

   TVSDK considers the given position to be the starting point for the asset. No seek operation is required. If the position is not inside the seekable range, TVSDK uses the default position.

   For example: 

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   
   ```
