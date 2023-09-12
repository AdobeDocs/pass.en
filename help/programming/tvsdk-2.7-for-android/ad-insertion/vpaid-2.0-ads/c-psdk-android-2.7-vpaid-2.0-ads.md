---
description: Video player ad-serving interface definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.
title: VPAID 2.0 ad support
exl-id: 24146e32-9021-4472-94f6-b3d4703f0f9a
---
# VPAID 2.0 ad support {#vpaid-ad-support}

Video player ad-serving interface definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.

The following features are supported:

* Version 2.0 of the VPAID specification

  For more information, refer to [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf). 
* Linear VPAID ads with video-on-demand (VOD) content 
* JavaScript VPAID ads

  VPAID ads must be JavaScript-based, and the ad response must identify the media type of the VPAID ad as `application/javascript`.

The following features are not supported:

* Version 1.0 of the VPAID specification
* Skippable ads
* Nonlinear ads, such as overlay ads, dynamic companion ads, minimizable ads, collapsible ads, and expandable ads
* Preloading VPAID ads
* VPAID ads in live content
* Flash VPAID ads

## API

The following API elements support VPAID 2.0 ads:

* The `getCustomAdView` method of `MediaPlayer` returns a `CustomAdView` object, representing the web view that renders the VPAID ad (see [API References](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` sets the timeout on the VPAID loading process. The default timeout value is 10 seconds.

While the VPAID ad is playing:

* The VPAID ad is displayed in a view container above the player view, so code that relies on taps by users on the player view does not work. 
* Calls to `pause` and `play` on the player instance pause and resume the VPAID ad. 

* VPAID ads do not have a predefined duration, because the ad can be interactive.

  The ad duration and total ad break duration that are specified in the ad server response might not be accurate.
