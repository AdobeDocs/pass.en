---
description: The ad timeline appropriate to one playing of VOD content may be inappropriate for subsequent plays. You can replace a VOD timeline without changing the content.
title: Changes to VOD
---

# Changes to VOD {#changes-to-vod}

The ad timeline appropriate to one playing of VOD content may be inappropriate for subsequent plays. You can replace a VOD timeline without changing the content.

Situations in which you might wish to replace a VOD timeline include:

* Replace local ads, but leave national ads during a C3 window.
* Replace burnt-in ads after the C3 window closes.
* Dynamically replace old C3 ads with newer ads of greater duration.
* Insert fewer ads or none at all.

You can replace the ad timeline by submitting a new ad insertion request with the original M3U8 file and a different value of the `pttimeline` query parameter. 