---
title: Facilitate HLS player switching to failover/backup streams
description: Apple HLS stack supports switching to failover/backup streams if it cannot retrieve any streams of the primary set. For Apple HLS devices, to facilitate failover, you can signal manifest server to treat primary and failover streams identified in the master playlist as disjoined sets (with their own UUIDs).
exl-id: 58c7a490-403f-41b2-bdbd-6f93e27083b0
---
# Facilitate HLS player switching to failover/backup streams {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS stack supports switching to failover/backup streams if it cannot retrieve any streams of the primary set. For Apple HLS devices, to facilitate failover, you can signal manifest server to treat primary and failover streams identified in the master playlist as disjoined sets (with their own UUIDs).

To facilitate switching to failover or backup streams on Apple HLS devices, you can specify the `ptfailover` parameter in the Bootstrap URL. If you provide this parameter, manifest server will create separate playback sessions (which determine the ads stitched) for each failover set.

## Details

How SSAI Handles HLS switching to failover/backup when you include `ptfailover=true` in the Bootstrap request:

* When a master playlist contains primary and backup sets:

  * The manifest server identifies AV stream URLs for different failover sets using the `BANDWIDTH` attribute and the parse order of AV stream URLs. It creates separate internal playback sessions (identified by separate UUIDs), and creates stream URLs pointing to manifest servers with the different UUIDs identifying different playback sessions.
  * The manifest server identifies I-Frame stream URLs for different failover sets using the matching `RESOLUTION` attribute and the parse order of I-Frame stream URLs. SSAI uses the UUIDs identifying the associated AV streams for I-Frame stream URLs pointing to SSAI.
  * For this feature, the manifest server only supports `EXT-X-MEDIA` groups without URI attributes in the master playlist.
  * The manifest server detects a 404 error response from a CDN with an `X-Object-Too-Old: true` header, and preserves the status code and the header when sending that response to the player.

* Pre-roll ads are only added to the primary set; they are completely disabled in the failover sets to avoid any erroneous and/or duplicated pre-roll ads when the player switches to failover streams.
