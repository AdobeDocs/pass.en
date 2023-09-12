---
description: In some cases, you need to know whether the media content is live or VOD.
title: Identify whether the content is live or VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
---
# Identify whether the content is live or VOD{#identify-whether-the-content-is-live-or-vod}

In some cases, you need to know whether the media content is live or VOD.

1. Ensure that the player is in at least the INITIALIZED status.
1. Determine whether the `MediaPlayerItem` content is live (true) or VOD (false).

   ```
   function get isLive():Boolean;
   ```
