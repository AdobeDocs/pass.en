---
title: Just-in-Time Transcoding
description: Just-in-Time Transcoding
copied-description: yes
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
---
# Just-in-Time Transcoding {#just-in-time-transcoding}

Primetime Ad Insertion features just-in-time transcoding and packaging to ensure that incompatible ad creatives can be played back properly in content streams. It can also inject ID3 packets into ad fragments that can be used in client-side ad tracking.
A typical workflow is as follows:

1. Adobe Primetime Ad Insertion fetches ads/creatives from the customer’s ad server.

1. If an ad’s creative format is natively compatible to the content stream, the creative is inserted into the manifest.

1. If an ad’s creative format is not natively compatible (e.g., .mp4, .mov, .webm), Primetime Ad Insertion searches for a pre- transcoded version of the ad from a specified CDN. If one is found, that ad is inserted; otherwise, the ad is queued for transcode.

1. After the ad creative is transcoded, Primetime Ad Insertion will stitch all subsequent requests for that ad asset into the manifests.

Primetime Ad Insertion supports transcoding for most video and linear formats. Ad creative transcoding typically occurs in less than three minutes. Please contact your Primetime support representative for more details.
