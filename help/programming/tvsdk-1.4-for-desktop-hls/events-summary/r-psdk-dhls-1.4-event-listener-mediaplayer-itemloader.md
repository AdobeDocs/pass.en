---
description: TVSDK dispatches media player item events in response to loading a media item.
title: Loader events
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
---
# Loader events{#loader-events}

TVSDK dispatches media player item events in response to loading a media item.

These events provide an alternative workflow. You are not required to implement this interface when creating a `MediaPlayer`. Use this when you want to have a `MediaPlayerItemLoader`.

To be notified about events related to loading a media player resource, register listeners for the following events with the `MediaPlayerItemLoader` object. 

|  Event  | Meaning  |
|---|---|
| MediaPlayerItemLoader.[completed](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed)  | Media resource loading completed successfully.  |
| MediaPlayerItemLoader.[failed](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed)  | A problem occurred with media resource loading.  |
