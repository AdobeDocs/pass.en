---
description: Video Player Ad-Serving Interface Definition (VPAID) provides a common interface to play video ads. VPAID provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.
title: Custom ad requirements
exl-id: c13748d6-23f1-4f34-95b4-7b532db6e536
---
# Custom ad requirements {#custom-ad-requirements}

The TVSDK player can play digital Video Player Ad-Interface Definition (VPAID) ads and display the ad loading status. If there are errors in the ad, or ads are taking too long to load, TVSDK ignores these ads.

Video Player Ad-Serving Interface Definition (VPAID) provides a common interface to play video ads. VPAID provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

The TVSDK supports the following features:

* Version 1.0 and 2.0 of the VPAID specification 
* Linear VPAID ads on video-on-demand (VOD) content 
* Flash VPAID ads

  VPAID ads must be Flash-based, and the ad response must identify the media type of the VPAID ad as `application/x-shockwave-flash`.

The following features are not supported:

* Nonlinear ads such as overlay ads and dynamic companion ads 
* Preloading VPAID ads 
* VPAID ads in live content 
* JavaScript VPAID ads

## Loading status {#section_5F55C0101CD44A65BCFE1D124CBDF239}

The TVSDK dispatches the following events:

* `AdLoading` 
* `AdLoaded` 
* `AdStarted` 
* `AdPlaying` 
* `AdStopped`

After the `AdStopped` event, the TVSDK resumes the video content.

>[!TIP]
>
>If you specify a value of zero, TVSDK attempts to load the ad until it loads or an error has occurred.

## Ignorning ads {#section_3EA452F420884335AE90DF23C17E416A}

If the ad takes too long to load or there are errors in the ad, the TVSDK can ignore the ad, and the next ad in the ad pod is automatically played.

If the `AuditudeSettings.customAdLoadTimeout` setting specifies a number of seconds greater than zero, the TVSDK attempts to load the ad to the specified duration. If it cannot load the ad, the ad is skipped. For example, if you configure `AuditudeSettings.customAdLoadTimeout:5`, the TVSDK attempts to load the ad for a maximum of 5 seconds. If the ad still does not load, it is ignored.
