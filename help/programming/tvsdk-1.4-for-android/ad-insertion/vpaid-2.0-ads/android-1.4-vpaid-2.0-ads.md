---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.
title: VPAID 2.0 ad support
exl-id: ee3e0cd9-463e-4de9-a94f-292e968b6f08
---
# VPAID 2.0 ad support {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.

The following features are supported:

* Version 2.0 of the VPAID specification

  For more information, refer to [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf). 
* Linear VPAID ads on video-on-demand (VOD) content 
* JavaScript VPAID ads

  VPAID ads must be JavaScript-based, and the ad response must identify the media type of the VPAID ad as `application/javascript`.

The following features are not supported:

* Version 1.0 of the VPAID specification 
* Skippable ads 
* Nonlinear ads such as overlay ads, dynamic companion ads, minimizable ads, collapsible ads, and expandable ads 
* Preloading VPAID ads 
* VPAID ads in live content 
* Flash VPAID ads

## API Changes {#section_D62F3E059C6C493592D34534B0BFC150}

The following changes were made to the API:

* A `getCustomAdView` function has been added in `MediaPlayer` and returns the web view that renders the VPAID ad.

  For more information about the `CustomAdView` object that is returned by this function, see [API References](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html). 

* A `CUSTOM_AD` event is dispatched from the media player instance.

  The application can register an event callback by implementing `CustomAdEventListener`. 

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` allows you to change the default timeout on the VPAID loading process.

  The default timeout value is 10 seconds.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

While the VPAID ad is playing:

* The VPAID ad is displayed in a view container above the player view, so the code that relies on taps by users on the player view does not work. 
* The main content player is paused, and calls to `pause` and `play` on the player instance are used to pause and resume the VPAID ad. 

* VPAID ads do not have a predefined duration, because the ad can be interactive.

  The ad duration and total ad break duration that are defined by the ad server response might not be accurate.

## Implement VPAID 2.0 integration {#implement-vpaid-integration}

To add VPAID 2.0 support, add a custom ad view and appropriate listeners.

To add VPAID 2.0 support: 

1. Add the custom ad view to the player interface.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Add a listener for custom ad events.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
