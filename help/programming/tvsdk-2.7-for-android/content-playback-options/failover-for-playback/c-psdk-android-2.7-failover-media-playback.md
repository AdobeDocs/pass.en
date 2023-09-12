---
description: For live and video-on-demand (VOD) media, TVSDK starts playback by downloading the playlist that is associated with the middle-resolution bit rate and downloads the media segments that are defined by that playlist. It quickly selects the high-resolution bit rate playlist and its associated media and continues the downloading process.
title: Media playback and failover
exl-id: 3da1bde3-b685-4331-8bbe-a4c8ccdc68ed
---
# Media playback and failover {#media-playback-and-failover}

For live and video-on-demand (VOD) media, TVSDK starts playback by downloading the playlist that is associated with the middle-resolution bit rate and downloads the media segments that are defined by that playlist. It quickly selects the high-resolution bit rate playlist and its associated media and continues the downloading process.

## Missing playlist failover {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

When an entire playlist is missing, for example, when the M3U8 file that is specified in a top-level manifest file does not download, TVSDK attempts to recover. If it cannot be recovered, your application determines the next step.

If the playlist that is associated with the middle-resolution bit rate is missing, TVSDK searches for a variant playlist at the same resolution. If it finds the same resolution, TVSDK starts downloading the variant playlist and the segments from the matching position. If the player does not find the same resolution playlist, it will try to cycle through other bitrate playlists and their variants. An immediately lower bitrate is the first choice, then its variant, and so on. If all of the lower bitrate playlists and their variants are exhausted in the attempt to find a valid playlist, TVSDK will go to the top bitrate and count down from there. If a valid playlist cannot be found, the process fails, and the player moves to the ERROR state.

Your application can determine how to handle this situation. For example, you might want to close the player activity and direct the user to the catalog activity. The event of interest is the `STATUS_CHANGED` event, and the corresponding callback is the `onStatusChanged` method. Here is code that monitors whether the player changes its internal status to `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## Missing segment failover {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

When a segment is missing, for example when a particular segment fails to download, TVSDK attempts to recover through a variety of failover attempts. If it cannot recover, it issues an error.

If a segment is missing on the server because, for example, the manifest file is not present, the segment cannot be downloaded, and so on, TVSDK attempts to fail over by attempting the following options:

1. Attempt a failover to the same segment, at the same bit rate, in a variant file. 
1. Switch to an alternate bit rate (ABR switch) in the same file. 
1. Cycle through every available bit rate in every available variant. 
1. Skip the segment and issue a warning.

When TVSDK cannot obtain an alternative segment, it triggers a `CONTENT_ERROR` error notification. This notification contains an inner notification with the `DOWNLOAD_ERROR` code. If the stream with the problem is an alternate audio track, TVSDK generates the `AUDIO_TRACK_ERROR` error notification.

If the video engine is continuously unable to obtain segments, it limits continuous segment skips to 5, after which playback is stopped and TVSDK issues a `NATIVE_ERROR` with the code 5.

>[!NOTE]
>
>Here are some restrictions you should be aware of:
>
>* The adaptive bit rate (ABR) control parameters are not taken into consideration when a failover occurs. 
>
>  This is because the failover mechanism is designed to use any of the currently available playlists, regardless of their bit rate profile, as backup streams. 
>* During a failover operation, there can be a profile switch. 
>
>  If an error occurs during the download of one of the playlist segments, ABR control parameters such as min/max allowed bit rate are ignored. 
>
