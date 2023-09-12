---
description: You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
title: Updating ad creative selection rules
exl-id: d52ac207-dbb9-49d7-bd04-b722159d0314
---
# Overview {#updating-ad-creative-selection-rules-overview}

You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.

When your video player makes a request to an ad server, the VAST/VMAP response usually includes multiple ad creatives ( `MediaFile` elements), each of which provides a URL to a different container-codec version. In some cases, ad creatives in the VAST/VMAP response each provide a different bitrate for the ad. If you want to specify your own priority and transformation rules for these ad creatives, you can do so in the [!DNL AdobeTVSDKConfig.json] configuration file.

>[!IMPORTANT]
>
>* Do not change the name of the TVSDK configuration file. The name must remain [!DNL AdobeTVSDKConfig.json]. 
>* This file must be placed in the [!DNL assets/] folder of your project. 
>

You can specify two types of rules in [!DNL AdobeTVSDKConfig.json]: *Priority* rules and *Normalize* rules.

## Disabling Pre-Roll {#disabling-preroll}

To disable pre-roll you will need to change the default opportunity generators to not make the pre-roll call. By default, TVSDK uses the following opportunity generators:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 

```

To disable the pre-roll on live streams, this should change to include only the SpliceOutOpportunityGenerator:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
