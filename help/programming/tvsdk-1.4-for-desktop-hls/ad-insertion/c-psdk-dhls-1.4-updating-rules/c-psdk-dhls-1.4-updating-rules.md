---
description: You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.
title: Updating ad creative selection rules
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
---
# Overview {#updating-ad-creative-selection-rules}

You can use the TVSDK configuration file (AdobeTVSDKConfig.json) to update the priorities for ad creative selection on VAST/VMAP responses. You can also use this configuration file to define the source URL transformation rules for ad creatives.

When your video player makes a request to an ad server, the VAST/VMAP response usually includes multiple ad creatives ( `MediaFile` elements), each of which provides a URL to a different container-codec version. In some cases, ad creatives in the VAST/VMAP response each provide a different bitrate for the ad. If you want to specify your own priority and transformation rules for these ad creatives, you can do so in the [!DNL AdobeTVSDKConfig.json] configuration file.

>[!IMPORTANT]
>
>* Do not change the name of the TVSDK configuration file. The name must remain [!DNL AdobeTVSDKConfig.json]. 
>* This file should be hosted on your content delivery network (CDN). 
>

You can specify two types of rules in [!DNL AdobeTVSDKConfig.json]: *Priority* rules and *Normalize* rules.
