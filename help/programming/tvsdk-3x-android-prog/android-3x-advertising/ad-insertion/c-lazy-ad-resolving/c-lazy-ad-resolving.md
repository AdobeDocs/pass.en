---
description: Ad resolving and ad loading may cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading and Lazy Ad Resolving features can reduce this startup delay. Lazy Ad Resolving has changed significantly in the 3.0 version. In Lazy Ad loading prior to 3.0, ad resolution was broken into two steps, resolving just pre-rolls ads prior to the PREPARED status, and mid-rolls and post-rolls after the PREPARED status. This has changed and ad breaks are now resolved at a specified interval prior to the position of the ad break.
keywords: Lazy;Ad resolving;Ad loading
title: Just-in-Time Ad Resolving
exl-id: 7ce0dcac-859b-4570-a31b-4ea1e10ccf95
---
# Overview {#just-in-time-ad-resolving-overview}

Ad resolving and ad loading may cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading and Lazy Ad Resolving features can reduce this startup delay. Lazy Ad Resolving has changed significantly in the 3.0 version. In Lazy Ad loading prior to 3.0, ad resolution was broken into two steps, resolving just pre-rolls ads prior to the PREPARED status, and mid-rolls and post-rolls after the PREPARED status. This has changed and ad breaks are now resolved at a specified interval prior to the position of the ad break.

* Basic ad resolving and loading process:

    1. TVSDK downloads a manifest (playlist) and *resolves* all of the ads. 
    1. TVSDK *loads* all of the ads and places them on the timeline. 
    1. TVSDK moves the player into the PREPARED status, and content playback begins.

  The player uses the URLs in the manifest to obtain the ad content (creatives), ensures that the ad content is in a format that TVSDK can play, and TVSDK places the ads on the timeline. This basic process of resolving and loading ads can cause an unacceptably long delay for a user waiting to play their content, especially if the manifest contains several ad URLs. 

* *Lazy Ad Loading*:

    1. TVSDK downloads a playlist and *resolves* all of the ads. 
    1. TVSDK *loads* pre-roll ads, moves the player into the PREPARED status, and content playback begins. 
    1. TVSDK *loads* the remaining ads and puts them on the timeline as playback occurs.

  This feature improves upon the basic process by putting the player into the PREPARED status before all ads are loaded. 

* *Lazy Ad Resolving*:

    1. TVSDK downloads the playlist. 
    1. TVSDK resolves and loads any pre-roll ads, moves the player into the PREPARED status, and content playback begins. 
    1. TVSDK resolves and each of the remaining ad breaks individually based on the following calculation:

       `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

       By default, for content with a 6 second Target duration, this will be 5.0 + 30.0 + 6.0 seconds (41 seconds) 
    
    1. If an ad break occurs within 10 seconds of the start position, it will get resolved along with pre-roll ads prior to the PREPARED status.

>[!IMPORTANT]
>
>**Factors to consider with Lazy Ad Resolving:**
>
>* Lazy Ad Resolving is only supported for VOD streams only with modes SERVER_MAP and MANIFEST_CUES. 
>* Lazy Ad Resolving is not enabled by default. If disabled, all ads are resolved on VOD streams before playback starts. 
>* Lazy Ad Resolving is incompatible with the Instant On feature. For more information about Instant On, see Instant On. 
>* With Lazy Ad Resolving, while seeking forward over an ad break, the closest ad break to the seek position will be resolved during the seek. 
>* With Lazy Ad Resolving, if multiple ad breaks exist at the same time (VMAP), they will be resolved at the same time. 
>* It is not recommended to reduce the value of *setDelayAdLoadingTolerance() *below the default value (5 seconds). Doing so could cause the player to "buffer" unnecessarily. 
>* Lazy Ad Resolving does not affect pre-roll ads. 
>* Lazy Ad Resolving is currently supported with the Auditude-Plugin. It is recommended to not set *setDelayAdLoading*to true if you are using a custom resolver.
>
