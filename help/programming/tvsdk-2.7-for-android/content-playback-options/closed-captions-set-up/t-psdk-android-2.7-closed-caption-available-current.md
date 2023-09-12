---
description: You can select a track from a list of currently available closed-caption tracks. This becomes the current track, which is displayed when visibility is on. Some tracks might not be available initially, so listen for the event that indicates that more have become available.
title: Select a current caption track from among available tracks
exl-id: d604dedc-f3c3-4c97-9b0f-84da326c0678
---
# Select a current caption track from among available tracks {#select-a-current-caption-track-from-among-available-tracks}

You can select a track from a list of currently available closed-caption tracks. This becomes the current track, which is displayed when visibility is on. Some tracks might not be available initially, so listen for the event that indicates that more have become available.

1. Wait for the media player to be in at least the `PREPARED` status.
1. Listen for these events:

    * `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZED`: The initial list of closed-caption tracks is available.

1. Get a list of all currently available closed-caption tracks.

   For example: 

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Select an available track to be the current track.

   For example: 

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

   Retrieve the list each time that the event occurs to ensure that you always have the most current list.
