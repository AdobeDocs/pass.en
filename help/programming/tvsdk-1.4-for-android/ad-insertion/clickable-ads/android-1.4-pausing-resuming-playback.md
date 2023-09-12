---
description: When a user clicks an ad, your application should pause playback of the main video content.
title: Pause and resume playback
exl-id: 06922c80-b5c1-4e0c-872b-9400e07cf613
---
# Pause and resume playback {#pause-and-resume-playback}

When a user clicks an ad, your application should pause playback of the main video content.

   Override the `onPause` and `onResume` from the Android Activity.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
    
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
               _savedPlayerState = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
           } 
       } 
   } 
    
   abandonAudioFocus(); 
   
   ```
