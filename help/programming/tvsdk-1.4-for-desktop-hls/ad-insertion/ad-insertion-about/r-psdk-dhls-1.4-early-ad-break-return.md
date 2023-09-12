---
description: For live stream ad insertion, you might need to exit from an ad break before all the ads in the break are played to completion.
title: Implementing an early ad break return
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
---
# Implementing an early ad break return{#implementing-an-early-ad-break-return}

For live stream ad insertion, you might need to exit from an ad break before all the ads in the break are played to completion.

>[!NOTE]
>
>You must subscribe to the splice out/in ad markers ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, and `#EXT-X-CUE`).

Here are some requirements to consider:

* Parse markers such as `EXT-X-CUE-IN` (or equivalent marker tag) that appear in the linear or FER streams.

  Register the markers as being the marker for ad early return point. Only play `adBreaks` until this marker position during playback, which override the duration of the `adBreak` marked by the leading `EXE-X-CUE-OUT` marker. 

* If two `EXT-X-CUE-IN` markers exist for the same `EXT-X-CUE-OUT` marker, the first `EXT-X-CUE-IN` marker that appears is the one that counts. 

* If the `EXE-X-CUE-IN` marker appears in the timeline without a leading `EXT-X-CUE-OUT` marker, the `EXE-X-CUE-IN` marker is discarded.

  In a live stream, if the leading `EXT-X-CUE-OUT` marker has just moved out of the window, the TVSDK will not respond to it. 

* When there is an early return from an ad break, the `adBreak` plays until the playhead returns to the original position when the ad break was supposed to end and resumes playing the main content from that position.

## SpliceOut and SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` and `SpliceIn` markers mark the begin and the end of the ad break. The duration of the `SpliceOut` type of the `EXE-X-CUE` marker might be zero and the `SpliceIn` type of `EXE-X-CUE` marker marks the end of the ad break. They appear in one tag and differ by type.

**One marker with different types**

For example, here is one marker with different types: 

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

In the one marker with different types example, if the duration of the `SpliceOut` type is zero, the `SpliceOut` and `SpliceIn` must work together for every ad break. Currently, a `SpliceOut` marker with a non-zero duration and doesn't need pairing `SpliceIn` markers is more typical.

**Two separate markers**

The more typical scenario is a `SpliceOut` marker with a non-zero duration and that does not need the pairing `SpliceIn` markers. Here, a pairing `SpliceIn` marker marks the end the ad break during ad break playback, but the ad break is cut short at the `SpliceIn` marker position, and the main content starts playing at this position.

For example, here are two separate markers: 

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```
