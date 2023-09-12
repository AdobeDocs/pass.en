---
description: Video player ad-serving interface definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.
title: VPAID 2.0 ad support
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
---
# VPAID 2.0 ad support {#vpaid-ad-support}

Video player ad-serving interface definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.

The following features are supported:

* Version 2.0 of the VPAID specification

  For more information, see [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Linear VPAID ads with video-on-demand (VOD) content 
* In Live content, Browser TVSDK supports pre-roll JavaScript VPAID ads.
* In Flash fallback mode, Browser TVSDK supports only Flash-based VPAID ads.
* Linear JavaScript VPAID ads

  VPAID ads must be JavaScript-based, and the ad response must identify the media type of the VPAID ad as `application/javascript`.

The following features are not supported:

* Version 1.0 of the VPAID specification
* Skippable ads
* Nonlinear ads, such as overlay ads, dynamic companion ads, minimizable ads, collapsible ads, and expandable ads.
* Preloading VPAID ads
* VPAID ads in live content
* Flash VPAID ads

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

The following API elements support VPAID 2.0 ads:

* The `getCustomAdView` method of `MediaPlayer` returns a `CustomAdView` object, which represents the web view that renders the VPAID ad.

  For more information about the `getCustomAdView` method, see [MediaPlayer API documentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` sets the timeout on the VPAID loading process.

  The default timeout value is 10 seconds.

* The API, `auditudeSettings.ignoreVPAIDAds`, allows you to ignore VPAID ads received from the Auditude server. The API does not work for Flash Fallback.

While the VPAID ad is playing:

* The VPAID ad is displayed in a view container above the player view, so code that relies on taps by users on the player view does not work.
* Calls to pause and play on the player instance pause and resume the VPAID ad.
* VPAID ads do not have a predefined duration, because the ad can be interactive.

  The ad duration and total ad break duration that are specified in the ad server response might not be accurate.
