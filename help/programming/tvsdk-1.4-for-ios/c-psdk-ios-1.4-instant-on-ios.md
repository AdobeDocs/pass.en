---
description: Instant-on preloads parts of the media on one or more channels. After a user selects or switches channels, the content starts sooner because some of the buffering has already completed.
title: Instant-on
exl-id: 3a1b2172-8036-40f1-86b6-8304ef771aa9
---
# Instant-on{#instant-on}

Instant-on preloads parts of the media on one or more channels. After a user selects or switches channels, the content starts sooner because some of the buffering has already completed.

When your player is in the `PTMediaPlayerStatusReady` status, call `prepareToPlay` to preload and process some of the content for later playback.

>[!TIP]
>
>If you do not call `prepareToPlay`, calling `play` automatically calls `prepareToPlay` first. The preloading and processing is completed at this time.

TVSDK completes some or all of the following tasks for `prepareToPlay`:

* If the metadata key `kSyncCookiesWithAVAsset` is set, TVSDK makes one request to the original M3U8 file to synchronize cookies. 
* Loads DRM metadata keys. 
* Creates and prepares some structures, elements, or assets that are needed for playing content.

>[!TIP]
>
>The `PTMediaPlayer` and `PTMediaPlayerItem` `prepareToPlay` methods are equal. To avoid creating a separate `PTMediaPlayer` instance for each asset, use the `PTMediaPlayerItem` method.

Instant-on helps you launch multiple media player instances, or media-player item loader instances, simultaneously in the background and buffer video streams in all of these instances. When a user changes the channel, and the stream has buffered properly, calling `play` on the new channel starts the playback sooner.
