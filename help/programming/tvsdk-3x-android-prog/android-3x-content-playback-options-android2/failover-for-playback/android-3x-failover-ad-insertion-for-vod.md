---
description: The video-on-demand (VOD) ad-insertion process consists of the ad resolving, ad insertion, and ad playback phases. For ad tracking, TVSDK must inform a remote tracking server about the playback progress of each ad. When unexpected situations arise, TVSDK takes appropriate action.
title: Advertising insertion and failover for VOD
exl-id: 0f5929eb-b6cf-4454-904a-2d4637177b68
---
# Advertising insertion and failover for VOD {#advertising-insertion-and-failover-for-vod}

The video-on-demand (VOD) ad-insertion process consists of the ad resolving, ad insertion, and ad playback phases. For ad tracking, TVSDK must inform a remote tracking server about the playback progress of each ad. When unexpected situations arise, TVSDK takes appropriate action.

## Ad-resolving phase {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK contacts an ad delivery service, such as Adobe Primetime ad decisioning, and attempts to obtain the primary playlist file that corresponds to the video stream for the ad. During the ad-resolving phase, TVSDK makes an HTTP call to the remote ad-delivery server and parses the server's response.

TVSDK supports the following types of ad providers:

* Metadata ad provider

  The ad data is encoded in plain-text JSON files. 
* Primetime ad decisioning ad provider

  TVSDK sends a request, including a set of targeting parameters and an asset identification number, to the Primetime ad decisioningback-end server. Primetime ad decisioningresponds with a synchronized multimedia integration language (SMIL) document that contains the required ad information. 
* Custom ad markers provider

  Handles the situation where ads are burned into the stream, from the server side. TVSDK does not perform the actual ad insertion, but it needs to keep track of the ads that were inserted on the server side. This provider sets the ad markers that TVSDK uses to perform the ad tracking.

One of the following failover situations can occur during this phase:

* The data cannot be retrieved because, for example, of the lack of connectivity or a server-side error, such as a resource cannot be found, and so on. 
* The data was retrieved, but the format is invalid.

  This might occur because, for example, the parsing of the inbound data failed.

TVSDK issues a warning notification about the error and continues processing.

## Ad-insertion phase {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserts the alternate content (ads) into the timeline that corresponds to the main content.

When the ad-resolving phase is complete, TVSDK has an ordered list of ad resources that are grouped into ad breaks. Each ad break is positioned on the main content timeline by using a start-time value that is expressed in milliseconds (ms). Each ad in an ad break has a duration property that is also expressed in ms. The ads in an ad break are chained, and as a result, the duration of an ad break is equal to the sum of the durations of the individual composing ads.

Failover can occur in this phase with conflicts that might occur on the timeline during ad insertion. For specific combinations of ad break start-time/duration values, ad segments might overlap. This overlap occurs when the last portion of an ad break intersects the beginning of the first ad in the next ad break. In these situations, TVSDK discards the later ad break and continues the ad-insertion process with the next item on the list until all ad breaks are inserted or discarded.

TVSDK issues a warning notification about the error and continues processing.

## Ad-playback phase {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK downloads the ad segments and renders them on the device's screen.

Now, TVSDK has resolved ads, positioned the ads on the timeline, and attempts to render the content on the screen.

The following main classes of errors might occur during the following phases:

* When connecting to the host server. 
* When downloading the manifest file. 
* When downloading the media segments.

TVSDK forwards the triggered events to your application, including notification events that are triggered when:

* A failover happens. 
* The profile is changed because of the failover algorithm. 
* All failover options have been considered, and no additional action can be taken automatically.

  Your application needs to take the appropriate action.

Regardless of whether errors occur, TVSDK calls `onAdBreakComplete` for each `onAdBreakStart` and `onAdComplete` for every `onAdStart`. However, if segments could not be downloaded, there might be gaps in the timeline. When the gaps are large enough, the values in the playhead position and the reported ad progress might exhibit discontinuities.
