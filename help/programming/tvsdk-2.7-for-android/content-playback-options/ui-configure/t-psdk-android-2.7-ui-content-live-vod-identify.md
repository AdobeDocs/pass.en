---
description: You might need to know whether the media content is live or video on demand (VOD).
title: Identify whether the content is live or VOD
exl-id: 756d4f04-d354-4194-80c9-c2ea6198a566
---
# Identify whether the content is live or VOD {#identify-whether-the-content-is-live-or-vod}

You might need to know whether the media content is live or video on demand (VOD).

1. Ensure that the player is in at least the `PREPARED` state.
1. Determine whether the `MediaPlayerItem` content is live ( `true`) or VOD ( `false`).

   ```java
   boolean isLive();
   ```
