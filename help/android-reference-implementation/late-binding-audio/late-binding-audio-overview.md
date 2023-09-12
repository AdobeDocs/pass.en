---
description: You can enable and build controls for late binding audio.
title: Overview
exl-id: be3b41c5-1c30-430c-9baa-06b6496aceb4
---
# Overview {#overview}

You can enable and build controls for late binding audio.

The HLS standard allows multi-format streams, which means we can keep the audio and video tracks of a stream separate from each other. The video track, with multiple renditions (e.g., 240p, 480p, 720p, and 1080p) and the audio tracks (e.g., English, Spanish, French, German) can be encoded separately. The media player then chooses the desired video and audio tracks and binds them on the fly, on the client side.

You can implement various workflows, depending on your player user interface. The general workflow for the Primetime player is as follows:

1. When the end user selects a video, a list of available audio tracks for that media item is populated.
1. When the user taps the Settings button on the UI, the audio track options are displayed.
1. When an audio track is selected, the track becomes the active audio track. 
1. The end user can tap the Settings button to switch back to the original audio track.
