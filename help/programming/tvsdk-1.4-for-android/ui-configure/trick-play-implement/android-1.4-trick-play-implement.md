---
description: When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.
title: Implement fast forward and rewind
exl-id: 58ed9a96-9617-4364-81d4-b404b23cf265
---
# Overview {#implement-fast-forward-and-rewind-overview}

When users fast forward or fast rewind through the media, they are in the trick play mode. To enter trick play mode, you need to set the MediaPlayer playback rate to a value other than 1.

To switch the speed, you must set one value. 

1. Move from normal play mode (1x) to trick play mode by setting the rate on the `MediaPlayer` to an allowed value.

    * The `MediaPlayerItem` class defines the allowed playback rates. 
    * TVSDK selects the closest allowed rate if the specified rate is not allowed.

   This example sets the player's internal playback rate to the requested rate.

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
    
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
    
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
    
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. You can optionally listen for rate-change events, which let you know when you requested a rate change and when a rate change actually happens.

       TVSDK dispatches the following events related to trick play:

    * `AdobePSDK.PSDKEventType.RATE_SELECTED` when the `rate` value changes to a different value. 
    
    * `AdobePSDK.PSDKEventType.RATE_PLAYING` when playback resumes at the selected rate.

       TVSDK dispatches both of these events when the player returns from trick-play mode to normal play mode.
