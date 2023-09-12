---
description: To display banner ads, you need to create banner instances and allow Browser TVSDK to listen for ad-related events.
title: Display banner ads
exl-id: 331c10a4-ae31-4d3b-aaca-9497e2970ecf
---
# Display banner ads {#display-banner-ads}

To display banner ads, you need to create banner instances and allow Browser TVSDK to listen for ad-related events.

Browser TVSDK provides a list of companion banner ads that are associated with a linear ad through the `AdobePSDK.PSDKEventType.AD_STARTED` event.

Manifests can specify companion banner ads by:

* An HTML snippet 
* The URL of an iFrame page 
* The URL of a static image or an Adobe Flash SWF file

For each companion ad, Browser TVSDK indicates which types are available for your application. 

Add a listener for the event `AdobePSDK.PSDKEventType.AD_STARTED` that does the following:
   1. Clears existing ads in the banner instance.
   1. Gets the list of companion ads from `Ad.getCompanionAssets`.
   1. If the list of companion ads is not empty, iterate over the list for banner instances.
   
      Each banner instance (an `AdBannerAsset`) contains information, such as width, height, resource type (html, iframe, or static), and data that is required to display the companion banner.   
   1. If a video ad has no companion ads booked with it, the list of companion assets contains no data for that video ad.
   1. Sends the banner information to a function on your page that displays the banners in an appropriate location.
   
      This is usually a `div`, and your function uses the `div ID` to display the banner. For example:

      Add the event listener:    
   
      ```js   
      _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
      ```

      Implement the listener handler:    
   
      ```js   
      private function onAdStarted(event:AdPlaybackEvent):void 
      { 
          // check if there are any companion banner 
          if (event.ad && event.ad.companionAssets  
                       && event.ad.companionAssets.length > 0) { 
               for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
                  if (ExternalInterface.available) { 
                      //-- call the java script that will handle the banner display. 
                      ExternalInterface.call('addBanner', banner.resourceType,  
                          banner.width, banner.height, banner.bannerData); 
                   } 
               } 
           }  
           //...        
      }
      ```

      Example of JavaScript to handle the display:    
   
      ```js   
      function displayCompanion (resourceType, width, height, data) { 
          console.log(resourceType + "," +  width + "," +  height); 
          var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
       
          // Assuming that there is an HTML element on the page  
          // with an id of "banner300x250", for example 
          if (bannerDiv !== null) { 
              bannerDiv.innerHTML = data; 
          } 
      }
      ```
