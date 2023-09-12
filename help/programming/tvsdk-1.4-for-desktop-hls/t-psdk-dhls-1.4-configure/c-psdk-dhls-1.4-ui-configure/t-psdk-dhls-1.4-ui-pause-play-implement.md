---
description: You can add TVSDK behavior to pause and play buttons.
title: Play and pause a video
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
---
# Play and pause a video{#play-and-pause-a-video}

You can add TVSDK behavior to pause and play buttons.

1. Create a pause/play button that does the following.
   1. Wait for your player to be in at least the PREPARED status.
   1. To start playback, call the TVSDK play method:

      ```   
      function play():void;
      ```

   1. To pause playback, call the TVSDK pause method:

      ```   
      function pause():void;
      ```

1. Use the callback for the `MediaPlayerStatusChangeEvent.STATUS_CHANGED` event to check for errors or to take other appropriate actions.

   TVSDK calls this callback when the pause or play method is called. TVSDK passes information about the status change in the callback, including the new status, such as PAUSED or PLAYING.
