---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 provides a common interface to play video ads. It provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content.
title: VPAID 2.0 ad support
exl-id: 6d29e53c-8fb4-4dd7-9859-8c105923bdef
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
* Post-roll VPAID ad

## API Changes {#section_D62F3E059C6C493592D34534B0BFC150}

The following changes were made to the API:

* `PTAuditudeMetadata` has a `customAdLoadTimeout` property to change the default timeout on the VPAID loading process.

  The default timeout value is 10 seconds. 

* `PTMediaPlayerCustomAdNotification` is dispatched from the `PTMediaPlayer` instance

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

While the VPAID ad is playing:

* The VPAID ad is displayed in a view container above the player view, so the code that relies on taps by users on the player view does not work. 
* The main content player is paused, and calls to `pause` and `play` on the player instance are used to pause and resume the VPAID ad. 

* VPAID ads do not have a predefined duration, because the ad can be interactive.

  The ad duration and total ad break duration that are defined by the ad server response might not be accurate.

## Implement VPAID 2.0 integration {#section_63C9C737367C4A0AB4D62E0DC2084141}

To add VPAID 2.0 support in your iOS application:

1. (Optional) Add a listener for custom ad events. 

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Optional) Display the notification. 

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
    
   }
   ```
