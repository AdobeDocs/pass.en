---
description: You can save the current playback position in a video and resume playing at the same position in a future session.
title: Save the video position and resume later
exl-id: a06897a6-bf57-4902-b1b4-e931419b56ba
---
# Save the video position and resume later{#save-the-video-position-and-resume-later}

You can save the current playback position in a video and resume playing at the same position in a future session.

Dynamically inserted ads differ between user sessions, so saving the position **with** spliced ads refers to a different position in a future session. TVSDK provides methods to retrieve the playback position while ignoring spliced ads. 

1. When the user quits a video, your application retrieves and saves the position in the video.

   >[!TIP]
   >
   >Ad durations are not included.

   Ad breaks can vary in each session due to ad patterns, frequency capping, and so on. The current time of the video in one session might be different in a future session. When saving a position in the video, the application retrieves the local time  . Use the `localTime` property to read this position , which you can save on the device or in a database on the server.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   For example, if the user is at the 20th minute of the video, and this position includes five minutes of ads, `currentTime` will `be` 1200 seconds, while `localTime` at this position will `be` 900 seconds.

1. Restore the user session when player activity resumes.

   TVSDK does not resume playback between TVSDK initializations because it does not save any information locally. Your application must implement this logic.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. To resume the video at the same position:

    * To resume playing the video from the position that was saved from a previous session, use `seekToLocal`.     
    
      >[!TIP]
      >
      >This method is called only with local time values. If the method is called with current time results, incorrect behavior occurs.

    * To seek to the current time, use `seek`.

1. When your application receives the `onStatusChanged` status change event, seek to the saved local time.
1. Provide the ad breaks as specified in the ad policy interface.
1. Implement a custom ad policy selector by extending the default ad policy selector.
1. Provide the ad breaks that must be presented to the user by implementing `selectAdBreaksToPlay`.

   When the player enters the PREPARED status, all ads are already resolved, so the `AdPolicyInfo.adBreakTimelineItem` property contains all ad breaks before the local time position. Your application can decide to play a pre-roll ad break and resume to the specified local time, play a mid-roll ad break and resume to the specified local time, or play no ad breaks.
