---
description: Browser TVSDK provides tools for creating an advanced video player application (your Primetime player), which you can integrate with other Primetime components.
title: Flash Failover
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
---
# Flash Failover {#flash-failover}

Browser TVSDK provides tools for creating an advanced video player application (your Primetime player), which you can integrate with other Primetime components.

Use your platform's tools to create a player and connect it to the media player view in Browser TVSDK, which has methods to play and manage videos. For example, Browser TVSDK provides play and pause methods. You can create user interface buttons on your platform and set the buttons to call those Browser TVSDK methods.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

In Browser TVSDK, your application interacts only with the `Primetime.js` API. The underlying Browser TVSDK implementation decides which player technology to use based on the current platform and the resource type of the media to be played.

The decision for the player technology is not made until you call `MediaPlayer.replaceCurrentResource` to play a specific resource.

For example:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determine the media player to use {#section_D844E386AF5848688D204DEE258ECEE6}

This sample procedure illustrates the process of determining the player technology: 

>[!TIP]
>
>The process might vary depending on the URL and your environment.

1. If Media Source Extensions is supported, use it with no known limitations. 
1. If supported, use the `<video>` tag directly without MSE. 
1. Ensure that you are using at least Adobe Flash Player version 23.0. 
1. If no suitable playback technology is found, `replaceCurrentResource` returns an error.

A subsequent `replaceCurrentResource` call on the same `MediaPlayer` instance follows the same process. This allows you to play various resource types by using the same `MediaPlayer` instance in the same parent `<DIV>` tag that you specified when the `MediaPlayerView` instance was created. 

>[!TIP]
>
>The SWF Object and the `<video>` tag are nested in the parent `<DIV>` tag.
