---
description: In Browser TVSDK, you can seek to a specific position (time) in a stream. A stream can be a sliding-window playlist or video-on-demand (VOD) content.
title: Handle seek when using the seek bar
exl-id: 4c09b218-917a-4318-82b0-c221d450a2c1
---
# Handle seek when using the seek bar{#handle-seek-when-using-the-seek-bar}

In Browser TVSDK, you can seek to a specific position (time) in a stream. A stream can be a sliding-window playlist or video-on-demand (VOD) content.

>[!IMPORTANT]
>
>Seeking in a live stream is allowed only for DVR.

1. Wait for Browser TVSDK to be in a valid state for seeking.

   Valid states are PREPARED, COMPLETE, PAUSED, and PLAYING. Being in a valid state ensures that the media resource has successfully loaded. If the player is not in a valid seekable state, attempting to call the following methods throws an `IllegalStateException`.

   For example, you can wait for Browser TVSDK to trigger  `AdobePSDK.MediaPlayerStatusChangeEvent`  with an `event.status` of `AdobePSDK.MediaPlayerStatus.PREPARED`. 

1. Pass the requested seek position to the `MediaPlayer.seek` method as a parameter in milliseconds.

   This moves the play head to a different position in the stream.

   >[!TIP]
   >
   >The requested seek position might not coincide with the actual computed position.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Wait for Browser TVSDK to trigger the  `AdobePSDK.PSDKEventType.SEEK_END`  event, which returns the adjusted position in the event's `actualPosition` attribute:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

    This is important because the actual start position after the seek could be different from the requested position. Some of the following rules might apply:

    * Playback behavior is affected if a seek, or other repositioning, ends in the middle of an ad break or skips ad breaks. 
    * You can seek only in the asset's seekable duration. For VOD, that is from 0 through the asset's duration.

1. For the seekbar that was created in the example above, listen for `setPositionChangeListener()` to see when the user is scrubbing:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
    
                       console.log("seek to " + time + " / " + duration); 
                   } 
    
               }); 
   
   ```

1. Set up event listener callbacks for changes in the user's seek activity.

       The seek operation is asynchronous, so Browser TVSDK dispatches these events related to seeking:

    * `AdobePSDK.PSDKEventType.SEEK_BEGIN` to indicate that seek is starting. 
    * `AdobePSDK.PSDKEventType.SEEK_END` to indicate that seeking was successful. 
    * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` to indicate that the media player has readjusted the seek position provided by the user.
