---
description: TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in both video on demand (VOD) and live streams.
title: Display a seek scrub bar with the current playback position
exl-id: a85a06d8-040e-435a-8f55-9df5af3babe1
---
# Display a seek scrub bar with the current playback position{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in both video on demand (VOD) and live streams.

>[!IMPORTANT]
>
>Seeking in a live stream is allowed only for DVR.

1. Set up callbacks for seeking.

       Seeking is asynchronous, so TVSDK dispatches the following seek-related events:

    * `SeekEvent.SEEK_BEGIN` - Seek starting. 
    * `SeekEvent.SEEK_END` - Seek successful. 
    * `SeekEvent.SEEK_POSITION_ADJUSTED` -  readjusted the seek position provided by the user.

1. Wait for the player to be in a valid status for seeking.

   Valid states are PREPARED, COMPLETED, PAUSED, and PLAYING. 

1. Listen for the appropriate event to see when the user is scrubbing.
1. Pass the requested seek position (milliseconds) to the `MediaPlayer.seek` method.

   ```
   function seek(position:Number):void;
   ```

   You can seek only in the asset's seekable duration. For video on demand, the duration is from 0 through the asset's duration.

   >[!TIP]
   >
   >This moves the play head to a new position in the stream, but the final computed position might differ from the specified seek position.

1. Wait for TVSDK to dispatch the `SeekEvent.SEEK_END` event.
1. Retrieve the final adjusted play position using event.actualPosition.

       This is important because the actual start position after the seek can be different from the requested position. Various rules might apply, including:

    * Playback behavior is affected if a seek or other repositioning ends in the middle of an ad break or skips ad breaks. 
    * If you seek near a segment boundary, the seek position is adjusted to the beginning of the segment.

1. Use the position information when displaying a seek scrub bar.
