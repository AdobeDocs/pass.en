---
description: You can add TVSDK behavior to pause and play buttons.
title: Play and pause a video
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
---
# Play and pause a video{#play-and-pause-a-video}

You can add TVSDK behavior to pause and play buttons.

1. Create a pause/play button that does the following.
   1. Wait for your player to be in at least the PREPARED state.
   1. To start playback, call the TVSDK play method:

      ```java   
      void play() throws IllegalStateException;
      ```

   1. To pause playback, call the TVSDK pause method:

      ```java   
      void pause() throws IllegalStateException;
      ```

1. Use the `MediaPlayer.PlaybackEventListener.onStateChanged` callback to check for errors or to take other appropriate actions.

   TVSDK calls this callback when the pause or play method is called. TVSDK passes information about the state change in the callback, including the new state, such as PAUSED or PLAYING.
