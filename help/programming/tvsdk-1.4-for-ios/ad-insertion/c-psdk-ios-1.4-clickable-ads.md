---
description: TVSDK provides you with information so that you can act on click-through ads. As you create your player UI, you must decide how to respond when a user clicks on a clickable ad.
title: Clickable ads
exl-id: eaaab835-884a-4d3f-b3be-e6f71c814985
---
# Clickable ads{#clickable-ads}

TVSDK provides you with information so that you can act on click-through ads. As you create your player UI, you must decide how to respond when a user clicks on a clickable ad.

In TVSDK for iOS, only linear ads are clickable.

## Respond to clicks on ads {#section_537AF2593FDB4257B81AAE2103B0C719}

When a user clicks on an ad, a companion banner ad, or a related button, your application must respond. TVSDK provides you with information about the destination URL for the click.

1. To set up an event listener for TVSDK, and provide the click-through information, add an observer for `PTMediaPlayerAdClickNotification`. 

   >[!NOTE]
   >
   >When a user clicks on an ad, a companion banner ad, or a related button, TVSDK dispatches this notification, including information about the destination for the click.

1. Monitor user interactions on clickable ads. 
1. When the user touches or clicks the ad or button, to notify TVSDK, use `[_player notifyClick:_currentAd.primaryAsset];`. 
1. Listen for the `PTMediaPlayerAdClickNotification` event from TVSDK. 
1. To retrieve the click-through URL and related information, use the `PTMediaPlayerAdClickURLKey` object. 
1. Pause the video. 
1. Use the click-through information to display the ad click-through URL and the related information. 

   >[!NOTE]
   >
   >You could, for example, display the information in one of the following ways:

    * In your application by opening the click-through URL in a browser.

      On desktop platforms, the video ad playback area is used to invoke click-through URLs at user clicks. 
    * Redirect users to their external mobile web browser.

      On mobile devices, the video ad playback area is used for other functions, such as hiding and showing controls, pausing playback, expanding to full screen, and so on. On these devices, a separate view, such as a sponsor button, is used to launch the click-through URL.

1. Close the browser window in which the click-through information is displayed and resume playing the video.

   For example: 

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   
   ```
