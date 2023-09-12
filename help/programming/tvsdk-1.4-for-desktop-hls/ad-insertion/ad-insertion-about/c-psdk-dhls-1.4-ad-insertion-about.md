---
description: Ad insertion resolves ads for video-on-demand (VOD) , for live streaming, and for linear streaming with ad tracking and ad playback. TVSDK makes the required requests to the ad server, receives information about ads for the specified content, and places the ads in the content in phases.
title: Inserting ads
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
---
# Overview {#inserting-ads-overview}

Ad insertion resolves ads for video-on-demand (VOD) , for live streaming, and for linear streaming with ad tracking and ad playback. TVSDK makes the required requests to the ad server, receives information about ads for the specified content, and places the ads in the content in phases.

An *`ad break`* contains one or more ads that play in sequence. TVSDK inserts ads in the main content as members of one or more ad breaks.

## Disable pre-roll ads {#disable-preroll-ads}

To disable pre-roll, change the default opportunity generators to not make the pre-roll call. The default opportunity generators is: 

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

To disable the pre-roll on live streams, change the above to include only the SpliceOutOpportunityGenerator: 

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
