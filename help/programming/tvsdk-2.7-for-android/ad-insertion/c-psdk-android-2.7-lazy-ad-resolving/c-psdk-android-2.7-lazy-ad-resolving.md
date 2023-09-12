---
description: Ad resolving and ad loading can cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading and Lazy Ad Resolving features can reduce this startup delay.
keywords: Lazy;Ad resolving;Ad loading
title: Lazy ad resolving
exl-id: 6f4c2b9b-a129-4132-8c88-259602222381
---
# Overview {#lazy-ad-resolving}

Ad resolving and ad loading can cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading and Lazy Ad Resolving features can reduce this startup delay.

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
    1. TVSDK resolves and loads the remaining ads and puts them on the timeline as playback occurs.

  Lazy Ad Resolving builds on Lazy Ad Loading to allow for even faster start up. After TVSDK places any pre-roll ads, it moves the player into the PREPARED status, and then resolves additional ads and places them on the timeline.

>[!IMPORTANT]
>
>Factors to consider with Lazy Ad Resolving:
>
>* Lazy Ad Resolving is enabled by default. If you disable it, all ads are resolved before playback starts. 
>* Lazy Ad Resolving does not allow seeking or trickplay until after all the ads are resolved:
>
>    * The player must wait for the `kEventAdResolutionComplete` event before allowing seeking or trick play.
>    * If the user attempts to perform seek or trick play operations while ads are still being resolved, TVSDK throws the `kECLazyAdResolutionInProgress` error.
>    * If necessary, the player should update the scrub bar, *after* receiving the `kEventAdResolutionComplete` event. 
>
>* Lazy Ad Resolving is for VOD only. It will not work with LIVE streams.
>* Lazy Ad Resolving is incompatible with the *Instant On* feature. 
>
>  For more information about Instant On, see  instant-on . 
>
>* While Lazy Ad Resolving results in playback starting much faster, if an ad break occurs in the first 60 seconds of playback, it may not get resolved.
>* Lazy ad resolution does not affect pre-roll ads.
