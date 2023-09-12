---
description: TVSDK provides you with information so that you can act on click-through ads. As you create your player UI, you must decide how to respond when a user clicks on a clickable ad.
title: Clickable ads
exl-id: 50c74c82-c5d8-43f6-accf-8330a426a7bd
---
# Clickable ads {#clickable-ads}

TVSDK provides you with information so that you can act on click-through ads. As you create your player UI, you must decide how to respond when a user clicks on a clickable ad.

For TVSDK for Flash Runtime, only linear ads are clickable.

## Respond to clicks on ads {#respond-to-clicks-on-ads}

When a user clicks an ad or a related button, your application is responsible for responding. TVSDK provides you with information about the destination URL.

This example shows one possible way to manage ad clicks. 

1. Each time an ad is played, display a button on top of the media player. A user who clicks the ad is redirected to the ad URL. This button is part of the [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. Include this overlay on our media player sample, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. To make the view visible only when an ad is playing, listen for the `onAdStart` and `onAdComplete` events dispatched by .

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. Monitor user interactions on clickable ads. When the user touches or clicks the ad or button, notify TVSDK with `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Listen for the `AdclickEvent.AD_CLICK` event.

   If an ad is playing, TVSDK dispatches the `AdClickEvent.AD_CLICK` event, from which you can retrieve the click-through URL and related information.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Pause the media player while directing the user to the ad URL.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Display the ad click-through URL and any related information.

       For example, you could display it in one of the following ways:

    * Open the click-through URL in a browser within your application.

      On desktop platforms, the video ad playback area is typically used for invoking click-through URLs upon user clicks. 
    * Redirect the user to the external mobile web browser.

      On mobile devices, the video ad playback area is used for other functions, such as hiding and showing controls, pausing playback, expanding to full screen, and so on. Therefore, on mobile devices, a separate view, such as a sponsor button, is usually presented to the user as a means to launch the click-through URL.

1. Close the browser window in which the click-through information is displayed and resume playing the video.
