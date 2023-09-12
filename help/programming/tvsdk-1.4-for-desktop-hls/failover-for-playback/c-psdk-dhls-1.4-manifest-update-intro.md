---
description: TVSDK can detect changed playback information in master m3u8 manifests for live streaming and update the playback information while the stream is playing. TVSDK supports a dynamic set of bit rate profiles as the profiles appear or disappear from the master manifest, including non-overlapping profile bit rates between updates.
title: Live master-manifest update
exl-id: e3fffe64-1d44-4227-b830-c7661478f067
---
# Live master-manifest update{#live-master-manifest-update}

TVSDK can detect changed playback information in master m3u8 manifests for live streaming and update the playback information while the stream is playing. TVSDK supports a dynamic set of bit rate profiles as the profiles appear or disappear from the master manifest, including non-overlapping profile bit rates between updates.

The following features are supported:

* Profile count (increasing or decreasing) 
* Profile bit rates (overlapping or not overlapping) 
* Profiles with URLs on the same (or different) servers 
* Any failover structure

All of the following conditions must be met:

* Stream is live. 
* Both the time and the etag change. 
* All rendition information remains the same (except that URLs may vary). 
* The DRM access information remains the same. 
* Segments are packaged around the same PTS and frame boundaries in a small error range.

## Live master-manifest update architecture {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

Here is some information and examples about how the TVSDK accommodates updated master manifests.

By default, this feature is turned off. If your application turns it on by setting an update frequency in minutes, the following steps occur after every update interval:

1. The TVSDK checks the master manifest's last modified time and etag to determine whether the file has been updated.

   If both the time and etag have changed, the file is deemed as modified. 
1. The TVSDK parses and analyzes the new manifest and takes appropriate action based on the nature of the update. 
1. If the current playing bit rate matches the bit rate of the modified manifest, the TVSDK switches to the new profile.

   The new profile could be from a different server or the same server, at the same bit rate. In this case, the transition is smooth. 
1. If the current playing bit rate is no longer present in the new manifest, the TVSDK tries to find a bit rate in the current profile that also exists in the new manifest.

    * If a match is found, the player first switches to the matching bit rate profile in the existing manifest and switches to the matching bit rate profile in the updated manifest. This ensures that the transition is smooth. 
    * If there is no bit rate in common between the previous manifest and the new manifest, or if the TVSDK cannot switch to the bit rate that matches, the TVSDK switches directly to the lowest bit rate profile of the new manifest and uses ABR to switch to any allowable bit rate based on bandwidth. This may cause a slight glitch in playback but should have minimal impact.

1. If the update is successful, the TVSDK dispatches a `MediaPlayerItemEvent.MASTER_UPDATED` event. 
1. If the update is not successful, playback continues with the set-up from before this update.

### Example 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

The following bit rates are broadcasting live:

* 500k 
* 900k 
* 2100k

The 2100k stream has some issues, so it needs to be restarted. The master manifest is updated to contain only 500k and 900k. Shortly afterwards, the users watching this program at 2100k will experience a bit rate switch down to 900k. The users watching at 900k continue to watch at 900k. Later, the 2100k stream resumes, and it is added back in the master manifest. A while later, the users who are watching at 900k, and have the bandwidth, are switched to 2100k.

### Example 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

The following bit rates are broadcasting live:

* 500k 
* 900k 
* 2100k

All of these bit rates need to be restarted. There are two temporal streams set up for this, at 400k and 1500k. The users are switched to 400k, which is the lowest bit rate of the new configuration. Some of the users are switched to 1500k when their bandwidth is sufficient. Later, the three bit rates are back up and the master manifest is updated. Users automatically switch back to watch at 500k, which is the lowest bandwidth in the revised (original) manifest. A while later, users are switched to the highest bandwidth (900k or 1200k) that their network allows.

## Use live master-manifest update {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

You can turn on this feature and check for related events.

1. To turn on live master-manifest updates, set the update frequency (in minutes) by setting the `NetworkConfiguration.masterUpdateInterval` property. 
1. Optionally, track successful manifest updates by listening for the `MediaPlayerItemEvent.MASTER_UPDATED` event.
