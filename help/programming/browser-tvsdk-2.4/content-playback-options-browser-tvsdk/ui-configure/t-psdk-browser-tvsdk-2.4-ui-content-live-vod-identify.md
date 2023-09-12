---
description: You might need to know whether the media content is live or VOD.
title: Identify whether the content is live or VOD
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
---
# Identify whether the content is live or VOD{#identify-whether-the-content-is-live-or-vod}

You might need to know whether the media content is live or VOD.

1. Wait for Browser TVSDK to trigger an `AdobePSDK.PSDKEventType.STATUS_CHANGED` event with an `event.status` of `AdobePSDK.MediaPlayerStatus.PREPARED`.

   This step ensures that the media resource has successfully loaded. 

   >[!IMPORTANT]
   >
   >If Browser TVSDK is not in at least the `PREPARED` state, attempting to call the following methods throws an `IllegalStateException`.

1. Read `live` from the `MediaPlayerItem` interface:

   ```js
   player.currentItem.live
   ```
