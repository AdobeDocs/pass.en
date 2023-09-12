---
description: You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
title: Update ad creative selection rules
exl-id: c11a7249-0036-4859-9e98-b0cac9ade5b1
---
# Overview {#update-ad-creative-selection-rules-overview}

You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.

When your video player makes a request to an ad server, the VAST/VMAP response usually includes multiple ad creatives ( `MediaFile` elements), each of which provides a URL to a different container-codec version. In some cases, ad creatives in the VAST/VMAP response each provide a different bitrate for the ad. If you want to specify your own priority and transformation rules for these ad creatives, you can do so in the [!DNL AdobeTVSDKConfig.json] configuration file.

>[!IMPORTANT]
>
>* Do not change the name of the TVSDK configuration file. The name must remain [!DNL AdobeTVSDKConfig.json]. 
>* This file must be placed in the [!DNL assets/] folder of your project. 
>* Changing audio tracks when ad is playing does not change the audio track. A player should not allow users to change the audio track when an ad is playing. 
>

You can specify two types of rules in [!DNL AdobeTVSDKConfig.json]: *Priority* rules and *Normalize* rules.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

The Ad rules are specified using a JSON file. The format of the JSON file remains the same in both versions of the TVSDK. However, in TVSDK v2.5, the Ad rules JSON file must be hosted on a location accessible via a HTTP URL. The application can use an instance of AuditudeSettings:

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  

```
