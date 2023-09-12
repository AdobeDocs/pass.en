---
description: TVSDK contacts an ad delivery service, such as Adobe Primetime ad decisioning, and attempts to obtain the primary playlist file that corresponds to the video stream for the ad. During the ad-resolving phase, TVSDK makes an HTTP call to the remote ad-delivery server and parses the server's response.
title: Ad-resolving phase
exl-id: 5dd96709-1a65-442f-a753-a4343c6e8762
---
# Ad-resolving phase{#ad-resolving-phase}

TVSDK contacts an ad delivery service, such as Adobe Primetime ad decisioning, and attempts to obtain the primary playlist file that corresponds to the video stream for the ad. During the ad-resolving phase, TVSDK makes an HTTP call to the remote ad-delivery server and parses the server's response.

 TVSDK supports the following types of ad providers:

* Metadata ad provider

  The ad data is encoded in plain-text JSON files. 
* Primetime ad decisioning ad provider

  TVSDK sends a request, including a set of targeting parameters and an asset identification number, to the Primetime ad decisioning back-end server. Primetime ad decisioning responds with a SMIL (synchronized multimedia integration language) document that contains the required ad information. 
* Custom ad markers provider

  Handles the situation where ads are burned into the stream, from the server side. TVSDK does not perform the actual ad insertion, but it needs to keep track of the ads that were inserted on the server side. This provider sets the ad markers that TVSDK uses to perform the ad tracking.

One of the following failover situations can occur during this phase:

* The data cannot be retrieved for reasons including a lack of connectivity or a server-side error, such as a resource cannot be found and so on. 
* The data was retrieved, but the format is invalid.

  This might occur because, for example, the parsing of the inbound data failed.

TVSDK issues a warning notification about the error and continues processing.
