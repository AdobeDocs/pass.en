---
description: When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, set the MediaPlayer playback rate to a value other than 1.
title: Implement fast forward and rewind
exl-id: 9e2dd250-a86d-4d75-8eba-385624af17af
---
# Overview {#implement-fast-forward-and-rewind}

When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, set the MediaPlayer playback rate to a value other than 1.

To switch the speed, you must set one value. 

1. Move from normal play mode (1x) to trick play mode by setting the rate on the `MediaPlayer` to an allowed value.

       Remember the following information:

    * The `MediaPlayerItem` class defines the allowed playback rates. 
    * TVSDK selects the closest allowed rate if the specified rate is not allowed.

       The following example sets the player's internal playback rate to the requested rate:     
    
       ```    
       import com.adobe.mediacore.MediaPlayer; 
       import com.adobe.mediacore.MediaPlayerItem; 
       import com.adobe.mediacore.MediaPlayerException; 
       import java.util.List; 
       import java.lang.Float; 
        
       private boolean setPlaybackRate(MediaPlayer player, float rate)  
         throws MediaPlayerException { 
           // Get list of playback rates that the media player supports 
           MediaPlayerItem item = player.getCurrentItem(); 
           if (item == null) return false; 
           List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
        
           // Return false if requested rate is not supported 
           if (availableRates.indexOf(rate) == -1) return false; 
        
           // Otherwise set the playback rate to the requested rate  
           // (this can throw MediaPlayerException) 
           player.setRate(rate); 
           return true; 
       }
       ```

1. You can optionally listen for rate-change events, which notifies you when you requested a rate change and when the rate change actually occurs.

  TVSDK dispatches the following events that are related to trick play:

* `MediaPlayerEvent.RATE_SELECTED`, when the `rate` value changes to a different value. 
    
* `MediaPlayerEvent.RATE_PLAYING`, when playback resumes at the selected rate.

  TVSDK dispatches these events when the player returns from trick play mode to normal play mode.
