---
description: To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure the way the player buffers.
title: Buffering time policies
exl-id: 78f1bb9f-3d10-4f05-90dd-5b52eee0feec
---
# Buffering time policies {#buffering-time-policies}

To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure the way the player buffers.

TVSDK defines a playback buffer length of at least 30 seconds and an initial buffer time within that, before the media starts playing, of at least 5 seconds. After the application calls `play` but before playback begins, TVSDK buffers the media up to the initial time to give a smooth start when it actually starts playing.

You can alter the buffer times by defining new buffering policies.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Depending on your environment (including the device, the operating system, or the network conditions), you can set different buffering policies for your player, such as changing the minimum duration for initial buffering and for ongoing playback buffering.

After you call `play`, the media player begins buffering the video. When the media player has buffered the amount of video specified by the initial buffer time, playback begins. This process improves the start-up time because the player does not wait for the entire playback buffer to fill before starting playback. Instead, after the few initial seconds are buffered, playback begins.

While the video is being rendered, TVSDK continues to buffer new fragments until it is has buffered the amount that is specified by the playback buffer time. If the current buffer length drops below the playback buffer time, the player will download additional fragments. Once the current buffer length is above the playback buffer time by a few seconds, TVSDK will stop downloading fragments.

>[!TIP]
>
>If the initial buffer value is high, it might give your user a long initial buffering time before starting. That might provide smooth playback for a longer time; however, if network conditions are poor, initial playback could be delayed.
