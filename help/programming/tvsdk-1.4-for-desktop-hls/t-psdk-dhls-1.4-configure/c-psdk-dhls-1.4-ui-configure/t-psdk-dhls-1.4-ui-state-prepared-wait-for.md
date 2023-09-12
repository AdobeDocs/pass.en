---
description: Before you can use most of the TVSDK player methods, the player must be in a valid status.
title: Wait for a valid state
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
---
# Wait for a valid state {#wait-for-a-valid-state}

With TVSDK you can control the basic playback experience for live and video on demand (VOD). TVSDK provides methods and properties on the player instance that you can use to configure the player user interface.Before you can use most of the TVSDK player methods, the player must be in a valid status.

The player moves through various statuses. Waiting for the player to be in the correct status ensures that the media resource has successfully loaded. If the player is not in at least the required status, many player methods throw throw `IllegalStateException`.

The required status is usually PREPARED. 

1. To confirm that the status is PREPARED:

   When the player is initializing, wait for TVSDK to call the callback for the `MediaPlayerStatusChangeEvent.STATUS_CHANGED` event with PREPARED status.

   To check whether the current status of the `MediaPlayer` object is at least PREPARED. 

   ```
   function getstatus():String;
   ```
