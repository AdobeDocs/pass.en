---
description: When playback reaches an ad break, passes an ad break, or ends in an ad break, TVSDK defines some default behavior for the positioning of the current playhead.
title: Customize playback with ads
exl-id: 3e945113-f44f-4b53-b952-10307f8d2d2f
---
# Overview {#customize-playback-with-ads-overview}

When playback reaches an ad break, passes an ad break, or ends in an ad break, TVSDK defines some default behavior for the positioning of the current playhead.

>[!TIP]
>
>You can override the default behavior by using the `AdBreakPolicySelector` class.

The default behavior varies, depending on whether the user passes the ad break during normal playback or by seeking in a video or repositioning it with fast forward or rewind (trick play).

You can customize ad playback behavior in the following ways:

* Save the position where the user stopped watching the video and resume playing at the same position in a future session. 
* If an ad break is presented to the user, display no additional ads for a number of minutes, even if the user seeks to a new position. 
* If the content fails to play after a few minutes, restart the stream or fail over to a different source for the same content.

  On the failover playback session, to allow the user to skip ads and resume to the previous failed position, you can disable pre-roll and/or mid-roll ads. TVSDK provides methods to enable skipping pre-roll and mid-roll ads.
