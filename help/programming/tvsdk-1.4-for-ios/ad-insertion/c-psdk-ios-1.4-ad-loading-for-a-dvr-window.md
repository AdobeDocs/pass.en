---
description: You can decide whether to resolve only the ads that occur after the user's current live point or to also resolve ads that occur before the current live point.
title: Load Ad for a DVR window
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
---
# Load Ad for a DVR window {#load-ad-for-a-dvr-window}

You can decide whether to resolve only the ads that occur after the user's current live point or to also resolve ads that occur before the current live point.

When a user starts to view content at the beginning of a DVR stream, TVSDK resolves all ads for the stream at that time. However, when the user starts to view content at a point after the beginning of the stream, you can decide whether to resolve only the ads that occur after the user's current live point or to also resolve ads that occurred before the current live point.

>[!TIP]
>
>Resolving ads after the current live point is faster, but if the user seeks backwards, this option prevents the player from playing ads that appeared earlier.

## Control ad loading for a DVR window {#section_2D93E2E947644D66B6F6ED1DD6742C25}

To control ad loading for a DVR window:

   To load all ads for the entire stream, set the `PTAdMetadata.enableDVRAds` property to `YES`. 

   >[!NOTE]
   >
   >The default value is `NO`, and this option loads ads only from the current live point.

   For example:

   ```
   PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
    
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
   adMetadata.zoneId = <ZoneId>; 
   adMetadata.domain = <Domain>; 
    
   // Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
   // (PTAuditudeMetadata is a subclass of PTAdMetadata)  
   adMetadata.enableDVRAds = YES; 
    
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
    
   //Create PTMediaPlayerItem with the previously prepared metadata    
   playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
   
   ```
