---
description: You can insert ads in your VOD and live/linear content by using the Adobe Primetime ad decisioning interface.
title: Advertising requirements
exl-id: 164a5e79-1634-4853-a2b9-d4b5bdbbf190
---
# Advertising requirements {#advertising-requirements}

You can insert ads in your VOD and live/linear content by using the Adobe Primetime ad decisioning interface.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime ad decisioning works with TVSDK to identify ad opportunities, resolve ads, and insert resolved ads in your video streams.

To incorporate ads in your video content, ensure that the advertising and main video content meets the following requirements:

* The advertising content's HLS version cannot be higher than the main content's HLS version. 
* Ads must be multiplexed and must contain an audio-only rendition, regardless of whether the main content is multiplexed. 
* Ad playlists should have the same bit-rate renditions as the renditions in the main content playlist. 
* The target duration and individual fragment duration of an ad cannot exceed the target duration of the main content. 
* If the main content contains an audio-only stream, the advertising content must also contain an audio-only stream. 
* If the main content contains subtitle streams, the advertising content must be unencrypted. 
* If the main content is multiple bit rate (MBR), the advertising content must also be MBR. 
* If the main content has alternate audio tracks, each ad must have at least one audio-only stream or the ads should be demuxed. If the ad neither has at least one audio-only stream nor is demuxed, the ad is skipped.
