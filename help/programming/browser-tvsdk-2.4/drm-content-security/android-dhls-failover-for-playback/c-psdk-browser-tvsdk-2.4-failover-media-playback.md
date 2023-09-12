---
description: For live and VOD media, Browser TVSDK starts playback by downloading the playlist that is associated with the middle-resolution bit rate and then downloading segments of the middle-resolution bit rate media that is defined by the playlist.
title: Media playback
exl-id: 56033ca2-8a63-4a0d-ac7d-bf208273a238
---
# Media playback {#media-playback}

For live and VOD media, Browser TVSDK starts playback by downloading the playlist that is associated with the middle-resolution bit rate and then downloading segments of the middle-resolution bit rate media that is defined by the playlist.

Browser TVSDK quickly selects the high-resolution bit rate playlist and its associated media and continues the downloading process.

## Missing playlist failover {#section_81A5822C108449E1A0E94A6E25DE9E8E}

When an entire playlist is missing, for example, when the M3U8 file specified in a top-level manifest file does not download, Browser TVSDK attempts to recover. If it cannot be recovered, your application determines the next step.

If the playlist that is associated with the middle-resolution bit rate is missing, Browser TVSDK searches for a variant playlist at the same resolution. If it finds the same resolution, it starts downloading the variant playlist and the segments from the matching position. If Browser TVSDK does not find the same resolution playlist, it will try to cycle through other bitrate playlists and their variants. An immediately lower bitrate is the first choice, then its variant, and so on. If all of the lower bitrate playlists and their variants are exhausted in the attempt to find a valid playlist, Browser TVSDK will go to the top bitrate and count down from there. If a valid playlist cannot be found, the process fails, and the player moves to the ERROR state.

Your application can determine how to handle this situation. For example, you might want to close the player activity and direct the user to the catalog activity. The event of interest is the status or state changed event, and the corresponding callback is the on status changed method. Here is code that monitors whether the player changes its internal state to ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 

```
