---
description: Full-event replay (FER) is a VOD asset that acts as a live/DVR asset, so your application must take steps to ensure that ads are placed correctly.
title: Enable ads in full-event replay
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
---
# Enable ads in full-event replay{#enable-ads-in-full-event-replay}

Full-event replay (FER) is a VOD asset that acts as a live/DVR asset, so your application must take steps to ensure that ads are placed correctly.

For live content, TVSDK uses the metadata/cues in the manifest to determine where to place ads. However, sometimes live/linear content might resemble VOD content. For example, when live content completes, an `EXT-X-ENDLIST` tag is appended to the live manifest. For HLS, the `EXT-X-ENDLIST` tag means that the stream is a VOD stream. TVSDK cannot automatically differentiate this stream from a normal VOD stream to correctly insert ads.

Your application must tell TVSDK whether the content is live or VOD by specifying the `AdSignalingMode`.

For a FER stream, the Adobe Primetime ad decisioning server should not provide the list of ad breaks that need to be inserted on the timeline before starting the playback. This is the typical process for VOD content. Instead, by specifying a different signaling mode, TVSDK reads all the cue points from the FER manifest and goes to the ad server for each cue point to request an ad break. This process is similar to live/DVR content.

In addition to each request that is associated with a cue point, TVSDK makes an additional ad request for pre-roll ads. 

1. From an external source, such as vCMS, obtain the signaling mode that should be used.
1. Create the advertising-related metadata.
1. If the default behavior must be overwritten, specify the `AdSignalingMode` by using `AdvertisingMetadata.setSignalingMode`.

   The valid values are `DEFAULT, SERVER_MAP`, and `MANIFEST_CUES`.

   You must set the ad signaling mode before calling `prepareToPlay`. After TVSDK starts to resolve and place ads on the timeline, changes to the ad signaling mode are ignored. Set the mode when you create the `AuditudeSettings` object. 

1. Continue to playback.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
