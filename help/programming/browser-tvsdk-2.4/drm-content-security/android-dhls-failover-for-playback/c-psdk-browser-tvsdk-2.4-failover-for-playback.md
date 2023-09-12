---
description: Streaming over the Internet requires a constant and stable connection to play a stream from a remote server. However, the variability of a viewer's Internet connection or streaming playback means that remote playback might not have the quality of media played locally.
title: Playback and failover
exl-id: 8316dfb8-3a2e-4057-a3d7-e3d8860e5bd4
---
# Playback and failover {#playback-and-failover}

Streaming over the Internet requires a constant and stable connection to play a stream from a remote server. However, the variability of a viewer's Internet connection or streaming playback means that remote playback might not have the quality of media played locally.

Primetime cannot protect from such failures as an ISP outage or a cable disconnection. However, Primetime streaming provides failover protection to protect playback from certain remote server failures or operational failures, making a better experience for viewers. Browser TVSDK implements failover protection to minimize playback interruptions and achieve a seamless playback despite transmission problems. The video player automatically switches to a backup media set when entire renditions or fragments are unavailable.

## Media playback {#media-playback}

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
