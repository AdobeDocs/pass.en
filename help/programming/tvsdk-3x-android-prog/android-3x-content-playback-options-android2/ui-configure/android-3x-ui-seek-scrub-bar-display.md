---
description: TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in video on demand (VOD) and live streams.
title: Display a seek scrub bar with the current playback position
exl-id: d5bc3a54-7dfd-435e-abb4-323639732e0a
---
# Display a seek scrub bar with the current playback position {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in video on demand (VOD) and live streams.

>[!TIP]
>
>Seeking in a live stream is allowed only for DVR.

1. Set up callbacks for seeking.

    Seeking is asynchronous, so TVSDK dispatches the following seek-related events:

    * `MediaPlayerEvent.SEEK_BEGIN`, where the seek starts. 
    * `MediaPlayerEvent.SEEK_END`, where the seek is successful. 
    * `MediaPlayerEvent.OPERATION_FAILED`, where the seek has failed.

1. Wait for the player to be in a valid status for seeking.

   The valid statuses are PREPARED, COMPLETE, PAUSED, and PLAYING.
1. Use the native `SeekBar` to set `OnSeekBarChangeListener`, which determines when the user is scrubbing.
1. Pass the requested seek position (milliseconds) to the `MediaPlayer.seek` method.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   You can seek only in the asset's seekable duration. For video on demand, that is from 0 through the asset's duration.

   >[!TIP]
   >
   >This step moves the play head to a new position in the stream, but the final computed position might differ from the specified seek position.

1. Listen for `MediaPlayerEvent.OPERATION_FAILED` and take appropriate actions.

   This event passes the appropriate warning. Your application determines how to proceed, and the options include trying the seek again or continuing playback from the previous position. 

1. Wait for TVSDK to call the `MediaPlayerEvent.SEEK_END` callback.
1. Retrieve the final adjusted play position using the callback's position parameter.

   This is important because the actual start position after the seek can be different from the requested position. Rules, including playback behavior is affected if a seek or other repositioning ends in the middle of an ad break or skips ad breaks, might apply. 

1. Use the position information when displaying a seek scrub bar.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Seeking Example**

In this example, the user scrubs the seek bar to seek to the desired position. 

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()), 
        playbackRange.getDuration()); 
     
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 

```
