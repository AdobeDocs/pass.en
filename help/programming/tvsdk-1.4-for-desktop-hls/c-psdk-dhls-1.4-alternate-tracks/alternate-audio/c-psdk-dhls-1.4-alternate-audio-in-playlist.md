---
description: The playlist for a video can specify an unlimited number of alternative audio tracks for the main video content. For example, you might want to add different languages to your video content or allow the user to switch between different tracks on their device while the content is playing.
title: Alternate audio tracks in the playlist
exl-id: dfd45f2d-8c8f-4c90-9c79-3afa03b518bf
---
# Alternate audio tracks in the playlist{#alternate-audio-tracks-in-the-playlist}

The playlist for a video can specify an unlimited number of alternative audio tracks for the main video content. For example, you might want to add different languages to your video content or allow the user to switch between different tracks on their device while the content is playing.

Alternate audio tracks, or late-binding audio, allows users to switch between multiple language tracks for HTTP video streams (live/linear and VOD), and you do not have to modify, duplicate, or repackage the video for each audio track. You can provide multiple language tracks for a video asset before or after the asset's initial packaging.

>[!TIP]
>
>For the alternate audio to be mixed with the video track of the main media, the timestamps of the alternate track must match the timestamps of the audio in the main track.

The main audio track is included in the audio tracks collection with the `default` label. Metadata for the alternate audio streams is included in the playlist in the `#EXT-X-MEDIA` tags with `TYPE=AUDIO`.

For example, an M3U8 manifest that specifies multiple alternate audio streams might look like this: 

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...

```
