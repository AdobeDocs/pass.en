---
description: Full Event Replay (FER) content is a live stream converted to VOD by adding the #EXT-X-ENDLIST tag to the end of the manifest file. The stream retains its ad cue markers.
title: FER ad resolving and insertion
exl-id: 9075932d-4e77-4249-af5d-0b392033907f
---
# FER ad resolving and insertion{#fer-ad-resolving-and-insertion}

Full Event Replay (FER) content is a live stream converted to VOD by adding the #EXT-X-ENDLIST tag to the end of the manifest file. The stream retains its ad cue markers.

Browser TVSDK treats a FER stream as VOD, so by default the ad signaling mode is `SERVER_MAP`. However, since the stream retains its ad cue markers, you can set the ad signaling mode to `MANIFEST_CUES`, which lets you use the ad cue markers for ad insertion.

To turn on ad insertion using cue markers for a FER stream: 

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER ad resolving and insertion behavior is similar to live ad resolving and insertion. Browser TVSDK does the following:

1. Inserts any pre-roll ads at the beginning of the content. 
1. Resolves ads specified by the cue points defined in the manifest. 
1. Replaces parts of the main content with ad breaks of the same duration 
1. Re-computes the virtual timeline, if necessary.

**Restriction:** Browser TVSDK supports only HLS FER streams playback. Also, MP4 mid-roll ads are not supported with FER streams.
