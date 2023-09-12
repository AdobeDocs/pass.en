---
description: TVSDK supports resolving and inserting ads for VOD and live/linear streams.
title: Primetime ad server metadata
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
---
# Overview {#primetime-ad-server-metadata-overview}

TVSDK supports resolving and inserting ads for VOD and live/linear streams.

## Prerequisite

Before you can include advertising in your video content, provide the following metadata information: 

* A `mediaID`, which identifies the specific content to play. 
* Your `zoneID`, which identifies your company or website. 
* Your ad server domain, which specifies the domain of your assigned ad server. 
* Other targeting parameters. 

## Set up Primetime ad server metadata {#section_86C4A3B2DF124770B9B7FD2511394313}

Your application must provide TVSDK with the required `PTAuditudeMetadata` information to connect to the ad server.

To set up the ad server metadata:

1. Create an instance of [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) and set its properties.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   
   ```

1. Set the `PTAuditudeMetadata` instance as metadata for the current `PTMediaPlayerItem` metadata by using `PTAdResolvingMetadataKey`. 

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Here is an example: 

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
    
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
    
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
    
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
    
       return metadata; 
   }
   ```
