---
description: You can save the current playback position in a video and resume playing at the same position in a future session.
title: Save the video position and resume later
exl-id: cf7111c1-7d9c-4f35-ac3d-d02c69c1524c
---
# Save the video position and resume later {#save-the-video-position-and-resume-later}

You can save the current playback position in a video and resume playing at the same position in a future session.

Dynamically inserted ads differ between user sessions, so saving the position **with** spliced ads refers to a different position in a future session. TVSDK provides methods to retrieve the playback position while ignoring spliced ads. 

1. When the user quits a video, your application retrieves and saves the position in the video.

   >[!TIP]
   >
   >Ad durations are not included.

   Ad breaks can vary in each session due to ad patterns, frequency capping, and so on. The current time of the video in one session might be different in a future session. When saving a position in the video, the application retrieves the local time, which you can save on the device or in a database on the server.

   For example, if the user is at the 20th minute of the video, and this position includes five minutes of ads, `getCurrentTime` will return 1200 seconds, while `getLocalTime` at this position will return 900 seconds.

   >[!IMPORTANT]
   >
   >Local time and current time are the same for live/linear streams. In this case, `convertToLocalTime` has no effect. For VOD, local time remains unchanged while ads play.

   ```java
   // Save the user session when player activity stops 
   @Override 
   public void onStop() { 
       super.onStop(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences( 
                 getActivity().getApplicationContext() 
               ); 
       SharedPreferences.Editor editor = prefs.edit(); 
       // get the local time where stream stopped playing and  
       // save it in System preferences 
       editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
       editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
       editor.commit(); 
       ... 
   } 
   
   ```

1. Restore the user session when player activity resumes.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs = PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil").equals(_contentInfo.toMediaResource().getUrl())) { 
    
           _lastKnownLocalTime = prefs.getLong(LAST_LOCAL_TIME, 0);    // get the last local time saved  
                                                                       // in system preferences 
           if (_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   
   ```

1. To resume the video at the same position:

    * To resume playing the video from the position that was saved from a previous session, use `seekToLocalTime`.     
    
      >[!TIP]
      >
      >This method is called only with local time values. If the method is called with current time results, incorrect behavior occurs.

    * To seek to the current time, use `seek`.

1. When your application receives the `onStatusChanged` status change event, seek to the saved local time.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if (_shouldResumePlayback) { 
               if(_lastKnownLocalTime >= 0) { 
                   _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
        ... 
   } 
   
   ```

1. Provide the ad breaks as specified in the ad policy interface.
1. Implement a custom ad policy selector by extending the default ad policy selector.
1. Provide the ad breaks that must be presented to the user by implementing `selectAdBreaksToPlay`.

   This method includes a pre-roll ad break and the mid-roll ad breaks before the local time position. Your application can decide to play a pre-roll ad break and resume to the specified local time, play a mid-roll ad break and resume to the specified local time, or play no ad breaks.
