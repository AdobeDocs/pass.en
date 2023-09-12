---
description: Media streams can carry additional metadata in the form of tags in the Media Presentation Description (MPD) file, and this file indicates the placement of advertising. You can specify custom tag names and be notified when certain tags appear in the manifest file.
title: Custom tags
exl-id: 9e6343b5-ade7-467a-b2a1-8f8d69492a1a
---
# Overview {#custom-tags-overview}

Media streams can carry additional metadata in the form of tags in the Media Presentation Description (MPD) file, and this file indicates the placement of advertising. You can specify custom tag names and be notified when certain tags appear in the manifest file.

## HLS content tags {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>This feature is not available for Safari on Apple computers, because Browser TVSDK uses the video tag, rather than Flash or MSE, to play HLS content.

Browser TVSDK provides out-of-the-box support for specific #EXT advertising tags. Your application can use custom tags to enhance the advertising workflow or to support blackout scenarios. To support advanced workflows, Browser TVSDK allows you to specify and subscribe to additional tags in the manifest. You can be notified when these tags appear in the manifest file.

>[!TIP]
>
>You can subscribe to custom tags both for VOD and live/linear streams.

>[!NOTE]
>
>When HLS is played by using the Video tag in Safari, and not by using Flash Fallback, this feature will not be available in Safari.

## Using custom HLS tags {#section_AD032318AEF5418393D2B1DF36B0BABB}

Here is an example of a customized VOD asset:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Your application can set up the following scenarios:

* A notification when `#EXT-X-ASSET` tags, or any other set of custom tag names to which you have subscribed, exist in the file. 
* Insert ads when an `#EXT-X-AD` tag, or any other custom tag name, is found in the stream.

You can subscribe to any of the following tags as custom tags: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. You are notified with a `TimedMetadata` event during parsing of manifest files.

There are some advertising tags, such as `EXT-X-CUE`, to which you are already subscribed. These ad tags are also used by the default opportunity generator. You can specify which ad tags are used by the default opportunity generator by setting the `adTags` property.

## DASH content tags {#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH has two ways of signalling events:

* In the MPD file.

  This file is similar to the M3U8 file in HLS content, and MPD events exist in the .mpd file. 
* Inband in the representation

  Inband events are multiplexed with representations by adding the event messages as part of the segments. A representation is a list of video and audio segments that are played in sequence. The inband event data is embedded in these segments.

These events are notified as `TimedMetadata` events to the application as soon as they are parsed by Browser TVSDK. Once an event is notified, it will not be notified again.
