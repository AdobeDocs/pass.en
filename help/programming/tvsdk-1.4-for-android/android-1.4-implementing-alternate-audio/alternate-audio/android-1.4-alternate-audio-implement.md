---
description: Late-binding audio uses MediaPlayer to play a video that is specified in an M3U8 HLS playlist and that can contain several alternate audio streams.
title: Access alternate audio tracks
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
---
# Access alternate audio tracks{#access-alternate-audio-tracks}

Late-binding audio uses MediaPlayer to play a video that is specified in an M3U8 HLS playlist and that can contain several alternate audio streams.

1. Wait for the MediaPlayer to be in at least the PREPARED state.
1. Listen for this event:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: The initial list of audio tracks is available. 

1. Get the available audio tracks from the `MediaPlayerItem` instance.

   `mediaPlayerItem.getAudioTracks()` 1. (Optional) Present the available tracks to the user.
1. Set the selected audio track on the `MediaPlayerItem` instance.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
