---
description: Here is an example of how a user can select a closed-caption track.
title: Allow the user to change the track
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
---
# Allow the user to change the track{#allow-the-user-to-change-the-track}

Here is an example of how a user can select a closed-caption track.

1. To display the available closed caption tracks, use the `MediaPlayerItem.closedCaptionsTracks` property.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. To set which closed-caption track is current, use the `MediaPlayerItem.selectClosedCaptionsTrack` method.
1. After the media player item is prepared, retrieve it from the media player by using the ` MediaPlayer.  currentItem ` method.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
    
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
