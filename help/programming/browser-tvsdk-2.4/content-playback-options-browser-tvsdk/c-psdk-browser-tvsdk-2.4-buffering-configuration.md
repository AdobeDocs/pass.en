---
description: To provide a smoother viewing experience, Browser TVSDK sometimes buffers the video stream. You can configure the way the player buffers.
title: Buffering
exl-id: 786379d1-0f2d-44a9-b580-1c8dcbd3fd17
---
# Buffering{#buffering}

To provide a smoother viewing experience, Browser TVSDK sometimes buffers the video stream. You can configure the way the player buffers.

Browser TVSDK defines a playback buffer length of at least 30 seconds and an initial buffer time within that, before the media starts playing, of at least 2 seconds. After the application calls `play` but before playback begins, Browser TVSDK buffers the media up to the initial time to give a smooth start when it actually starts playing.

## Set buffering times {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

The MediaPlayer provides methods to set and get the initial buffering time and playback buffering time.

>[!TIP]
>
>If you do not set the buffer control parameters before beginning playback, the media player defaults to 2 seconds for the initial buffer and 30 seconds for the ongoing playback buffer time.

* To use the buffer parameters, use the MediaPlayer's `bufferControlParameters` attribute.

  For example, to set the initial buffer to 2 seconds and the playback buffer time to 30 seconds:

  ```js
  var params = new AdobePSDK.BufferControlParameters(2000, 30000);
  ```

## Buffering time policies {#section_7EF2947931654CCC8DAB9172391FA4EB}

Depending on your environment (including the device, the operating system, or the network conditions), you can set different buffering policies for your player, such as changing the minimum duration for initial buffering and for ongoing playback buffering.

After you call `play`, the media player begins buffering the video. When the media player has buffered the amount of video specified by the initial buffer time, playback begins. This process improves the start-up time because the player does not wait for the entire playback buffer to fill before starting playback. Instead, after the few initial seconds are buffered, playback begins.

While the video is being rendered, Browser TVSDK continues to buffer new fragments until it is has buffered the amount that is specified by the playback buffer time. If the current buffer length drops below the playback buffer time, the player will download additional fragments. Once the current buffer length is above the playback buffer time by a few seconds, Browser TVSDK will stop downloading fragments.

>[!TIP]
>
>If the initial buffer value is high, it might give your user a long initial buffering time before starting. That might provide smooth playback for a longer time; however, if network conditions are poor, initial playback could be delayed.
