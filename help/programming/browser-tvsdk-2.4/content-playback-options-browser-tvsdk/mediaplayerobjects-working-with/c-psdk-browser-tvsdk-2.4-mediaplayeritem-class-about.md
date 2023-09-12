---
description: After a MediaResource is successfully loaded, Browser TVSDK creates an instance of the MediaPlayerItem class to provide access to that resource.
title: About the MediaPlayerItem class
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
---
# About the MediaPlayerItem class{#about-the-mediaplayeritem-class}

After a MediaResource is successfully loaded, Browser TVSDK creates an instance of the MediaPlayerItem class to provide access to that resource.

The `MediaResource` represents a request that is issued by the application layer to the `MediaPlayer` instance to load content.

The `MediaPlayer` resolves the media resource, loads the associated manifest file, and parses the manifest. This is the asynchronous part of the resource loading process. The `MediaPlayerItem` instance is produced after the resource has been resolved, and this instance is a resolved version of a `MediaResource`. Browser TVSDK provides access to the newly created `MediaPlayerItem` instance through `MediaPlayer.CurrentItem`.

>[!TIP]
>
>You must wait for the resource to be successfully loaded before accessing the media player item.
