---
description: There are a few ways to determine ad insertion and ad placement.
title: Ad insertion and placement
exl-id: 73f24a65-4be2-47d3-8cb9-5cb2c81e6d93
---
# Ad insertion and placement{#ad-insertion-and-placement}

There are a few ways to determine ad insertion and ad placement.

## Ad insertion {#section_1F7581B987704E318E064082190E8243}

Here is an overview of the process used to determine ad insertion:

1. **Opportunity detection**: The TVSDK uses stream information to detect possible and desired locations for ads. 
1. **Ad resolution**: The TVSDK communicates with an advertisement server to retrieve the ads to splice into the content. 
1. **Ad placement**: The TVSDK loads the specified ads and places them in ad breaks on the content timeline at the specified locations and recomputes the virtual timeline, if necessary.

## Ad placement {#section_B9D63F7409A2447F9FF209289BE5D3D5}

The TVSDK can get locations for possible ad placement from the following sources:

* **Manifest metadata/cues**

  The TVSDK detects the cues, extracts the necessary information from these cues, and communicates with an advertising server to get the corresponding ads. This source is common for live/linear streams.

  The TVSDK usually replaces main content with the ads at the location that is indicated by the metadata/cues; otherwise, the client would drop more and more behind the actual live point. 

* **The advertising server map**

  Usually, metadata about these streams is registered in the advertising server before playback. The TVSDK retrieves the ad timeline and corresponding ads from the server. This source is common for VOD streams.

  The TVSDK usually inserts the resolved ads into the main content as indicated by the server map.

>[!NOTE]
>
>By default, the TVSDK uses manifest cues for live/linear streams and advertising server maps for VOD streams. However, to support full-event replay for live events, your application must take extra steps.
