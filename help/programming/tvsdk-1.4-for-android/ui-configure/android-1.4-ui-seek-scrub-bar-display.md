---
description: TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in both video on demand (VOD) and live streams.
title: Display a seek scrub bar with the current playback position
exl-id: 8076521b-579d-491f-97de-c7b57daa9b2e
---
# Display a seek scrub bar with the current playback position {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supports seeking to a specific position (time) where the stream is a sliding-window playlist, in both video on demand (VOD) and live streams.

>[!IMPORTANT]
>
>Seeking in a live stream is allowed only for DVR.

1. Set up callbacks for seeking.

       Seeking is asynchronous, so TVSDK dispatches the following seek-related events:

    * `QOSEventListener.onSeekStart` - Seek starting. 
    * `QOSEventListener.onSeekComplete` - Seek successful. 
    * `QOSEventListener.onOperationFailed` - Seek failed.

1. Wait for the player to be in a valid state for seeking.

   Valid states are PREPARED, COMPLETE, PAUSED, and PLAYING. 

1. Use the native SeekBar to set `OnSeekBarChangeListener` to see when the user is scrubbing.
1. Listen for `QOSEventListener.onOperationFailed` and take appropriate actions.

   This event passes the appropriate warning. Your application determines how to proceed, for instance, by trying the seek again or continuing playback from the previous position. 

1. Wait for TVSDK to call the `QOSEventListener.onSeekComplete` callback.
1. Retrieve the final adjusted play position using the callback's position parameter.

   This is important because the actual start position after the seek can be different from the requested position. Playback behavior might be affected if a seek or other repositioning ends in the middle of an ad break or skips ad breaks. 

1. Use the position information when displaying a seek scrub bar.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Seeking Example**

In this example, the user scrubs the seek bar to seek to the desired position. 

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
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
