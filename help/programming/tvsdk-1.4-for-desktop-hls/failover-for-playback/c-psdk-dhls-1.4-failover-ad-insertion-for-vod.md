---
description: The video-on-demand (VOD) ad-insertion process consists of the ad resolving, ad insertion, and ad playback phases. For ad tracking, TVSDK must inform a remote tracking server about the playback progress of each ad. When unexpected situations arise, it takes appropriate action.
title: Advertising insertion and failover for VOD
exl-id: 5af5bef6-e948-4215-a89f-ee46fd2d8a38
---
# Advertising insertion and failover for VOD{#advertising-insertion-and-failover-for-vod}

The video-on-demand (VOD) ad-insertion process consists of the ad resolving, ad insertion, and ad playback phases. For ad tracking, TVSDK must inform a remote tracking server about the playback progress of each ad. When unexpected situations arise, it takes appropriate action.

## Ad-resolving phase {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK contacts an ad delivery service, such as Adobe Primetime ad decisioning, and attempts to obtain the primary playlist file that corresponds to the video stream for the ad. During the ad-resolving phase, TVSDK makes an HTTP call to the remote ad-delivery server and parses the server's response.

TVSDK supports the following types of ad providers:

* Metadata ad provider

  The ad data is encoded in plain-text JSON files. 
* Primetime ad decisioning ad provider

  TVSDK sends a request, including a set of targeting parameters and an asset identification number, to the Primetime ad decisioning back-end server. Primetime ad decisioning responds with a SMIL (synchronized multimedia integration language) document that contains the required ad information.

One of the following failover situations can occur during this phase:

* The data cannot be retrieved for reasons including a lack of connectivity or a server-side error, such as a resource cannot be found and so on. 
* The data was retrieved, but the format is invalid.

  This might occur because, for example, the parsing of the inbound data failed.

TVSDK issues a warning notification about the error and continues processing.

## Ad-insertion phase {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK inserts the alternate content (ads) into the timeline that corresponds to the main content.

When the ad-resolving phase is complete, TVSDK has an ordered list of ad resources that are grouped into ad breaks. Each ad break is positioned on the main content timeline using a start-time value that is expressed in milliseconds (ms). Each ad in an ad break has a duration property that is also expressed in ms. The ads in an ad break are chained together one after another. As a result, the duration of an ad break is equal to the sum of the durations of the individual composing ads.

Failover can occur in this phase with conflicts that might occur on the timeline during ad insertion. For specific combinations of ad break start-time/duration values, ad segments might overlap. The overlap occurs when the last portion of an ad break intersects the beginning of the first ad in the next ad break. In these situations,  discards the later ad break and continues the ad-insertion process with the next item on the list until all ad breaks are inserted or discarded.

TVSDK issues a warning notification about the error and continues processing.

## Ad-playback phase {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK downloads the ad segments and renders them on the device's screen.

At this point, TVSDK has resolved ads, positioned them on the timeline, and attempts to render the content on the screen.

The following main classes of errors might occur in this phase:

* Errors when connecting to the host server 
* Errors when downloading the manifest file 
* Errors when downloading the media segments

For all three error classes, TVSDK forwards triggered events to your application, including:

* Notification events triggered when a failover happens. 
* Notification events when the profile is changed because of the failover algorithm. 
* Notification events triggered when all failover options have been considered, and no additional action can be taken automatically.

  Your application needs to take the appropriate action.

Whether or not errors occur, TVSDK calls `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` for each `AdBreakPlaybackEvent.AD_BREAK_STARTED` and `AdPlaybackEvent.AD_COMPLETED` for every `AdPLaybackEvent.AD_STARTED`. However, if segments could not be downloaded, there might be gaps in the timeline. When the gaps are large enough, the values in the playhead position and the reported ad progress might exhibit discontinuities.
