---
description: By default, when starting playback, VOD media starts at 0 and live media starts at the client live point (DefaultMediaPlayer.LIVE_POINT).
title: Enter a stream at a specific time
exl-id: b97dbabf-e2ab-4669-a9f3-9129af938a40
---
# Enter a stream at a specific time{#enter-a-stream-at-a-specific-time}

By default, when starting playback, VOD media starts at 0 and live media starts at the client live point (DefaultMediaPlayer.LIVE_POINT).

   Pass a position to `MediaPlayer.prepareToPlay`.

   TVSDK considers the given position to be the starting point for the asset. No seek operation is required. If the position is not inside the seekable range,  uses the default position.

   For example: 

   ```
   var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
   if (seekableRange.contains(desiredSeekPosition) { 
       _mediaPlayer.seek(desiredSeekPosition); 
   }
   ```
