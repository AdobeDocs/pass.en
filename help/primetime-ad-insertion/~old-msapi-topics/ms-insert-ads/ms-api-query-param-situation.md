---
description: Beyond the basic query parameters, optional query parameters enable the manifest server to work with different clients and situations.
title: Optional query parameters by client and situation
---

# Optional query parameters by client and situation {#optional-query-parameters-by-client-and-situation}

Beyond the basic query parameters, optional query parameters enable the manifest server to work with different clients and situations.

## Ad insertion with Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

On the Akamai content delivery network (CDN), the Akamai Edge server works as an intermediary between the client and the manifest server. If you also use Ad Scaler, the `ptassetid` and `live` query parameters provide required information to Akamai Edge.

The `ptassetid` parameter is the publisher's ID for its asset. Akamai uses this, rather than the base64-encoded URL that you supply as part of the request URL, to identify the playlist to provide to the manifest server for ad insertion.

The `live` parameter distinguishes between live content and video on demand (VOD). The manifest server needs this information to support its streamlined interface with Akamai.

Here is a sample URL showing the parameters that pertain to Akamai: 

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Ad insertion from TVSDK on Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

A player based on Primetime TVSDK on Xbox need not supply additional query parameters beyond the basic ones.

## Ad insertion from TVSDK on iOS with Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

A player based on Primetime TVSDK on iOS using the Safari browser must specify the `ptplayer` and `live` parameters in addition to the basic query parameters.

The manifest server recognizes the `ptplayer` value `ios-mobileweb` and eliminates the pre-roll from the ad-stitched manifest it returns.

The `live` parameter tells the manifest server whether to return live or VOD content.

Here is a sample URL showing the parameters that pertain to iOS with Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Ad insertion using a custom ad cue format {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe provides names for ad cue formats that it does not support directly in the Primetime package. To use such a format, supply its Adobe-provided name as the value of the `ptcueformat` parameter.

Here is a sample URL specifying a custom ad cue format:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Ad insertion using ad cues to create a FreeWheel timeline for VOD {#section_E0D830F5EEE24639819B975B90F6999F}

For VOD content containing ad cues to be parsed and included in a FreeWheel ad request, set the value of the `ptcueformat` parameter to `DPIsimple`.

Here is a sample URL that specifies using a FreeWheel timeline for VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Ad insertion using a custom timeline for VOD {#section_F398F7659164463FA886A4CC787C7B5A}

To ask the manifest server to insert ads into VOD content according to a timeline you supply, set the value of the `pttimeline` parameter to a string specifying the timeline. See [VOD timeline format](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Here is a sample URL that uses a custom timeline for VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

It specifies an initial break of one minute containing up to two ads, followed by a two-minute content segment, followed by a 30-second break containing up to two ads, followed by a five-minute content segment.

Ad stitching for a custom content timeline for VOD content behaves as follows:

* The ad appears at the closest break boundary after the ad placement time specified by the ad server.

* Segments are at least two seconds long.

## Authorizing TS segments {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe supports this feature only for the Akamai CDN. HTTP live streaming (HLS) delivers transport stream (TS) segments using a stream-level M3U8 playlist. Multiple stream-level playlists are provided to the client in a variant M3U8 playlist. The client picks one playlist stream from the variant list, then downloads TS segments in that stream-level playlist one-by-one. In normal operation, the requested content can require cookie authorization, which the manifest server handles invisibly in the background. It extracts the cookie from the raw content and appends an appropriate token to the URL to be used in requesting the selected playlist stream.

When the Bootstrap URL query parameters include `pttoken=true`, the publisher requires a cookie to be used in requesting each TS segment, rather than just once for the whole stream. The manifest server attaches this cookie as a query parameter to each TS segment URL in the stream playlist it sends back.
