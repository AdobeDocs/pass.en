---
description: You can add pause and play buttons to pause or play your video.
title: Play and pause a video
exl-id: cb13ae62-f96b-4329-841f-aba885725d70
---
# Play and pause a video {#play-and-pause-a-video}

You can add pause and play buttons to pause or play your video.

1. To create a pause or play button:
   1. Wait for the player to be in at least the prepared state.
   1. To start playback, call the `play` method:

      ```java   
      void play() throws MediaPlayerException;
      ```

   1. To pause playback, call the `pause()` method:

      ```java   
      void pause() throws MediaPlayerException;
      ```

1. Use the status changed event callback to check for errors or to take other appropriate actions.

   TVSDK calls this callback for `pause()` or `play()` and passes information about the status change, including the new status, such as paused or playing.
