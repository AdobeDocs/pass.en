---
title: Use Ad Insertion for VOD
description: Using Ad Insertion for VOD
exl-id: c998938e-f8a6-4ad3-97f6-ca4ad5055f15
---
# Use Ad Insertion for VOD {#ad-insertion-vod}

Primetime Ad Insertion supports ad insertion into multiple VOD assets, using standard VAST 3.0+ or VMAP 1.0+ formats.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (Ad maps) {#server-mapped-ads}

Primetime Ad Insertion supports VOD insertion with ads inserted prior to the beginning of playback using ad timelines information defined in a VMAP format.  VMAP-specific ad tracking such as breakStart/breakEnd beacons will be delivered with [Ad Tracking](set-up-ad-tracking.md).

## Full Event Replay (VOD with Ad Decisioning Cues) {#full-event-replay}

Primetime Ad Insertion also supports specialized VOD assets that contain cues in the content stream itself, such as found in playback of previously recorded live events. For more information on the types of ad decision cues (or cue formats) we support, see [Using Ad Insertion in Live/Linear](ad-insertion-live-linear-stream.md).

We support both single ad-request and parallel multiple ad-request scenarios for VOD assets containing more than one ad break. For more information, see `ptmulticall` parameter in [Parameter description](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Both VAST and VMAP formats are supported for in-stream cues.
