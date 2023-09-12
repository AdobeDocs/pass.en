---
description: The MediaPlayer provides a notifyClick() function that dispatches ad-related events when a clickable ad is playing. These events provide ad and ad break information that your app can use to provide click-through functionality.
title: Handle Clickable Ads
exl-id: 25738592-f3fe-4f13-b2bb-26a5f942cd18
---
# Handle Clickable Ads {#handle-clickable-ads}

The MediaPlayer provides a notifyClick() function that dispatches ad-related events when a clickable ad is playing. These events provide ad and ad break information that your app can use to provide click-through functionality.

The MediaPlayer fires the following events when a clickable ad plays:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

The `AdClickedEvent` contains the information necessary to process the click-through function.

1. Provide a control in your player for users to click on clickable ads.

   This could be a button or any other element for capturing the user's click.
1. Add an event listener for the user's ad click event.

   For example: 

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   
   ```

1. Add a handler for the user's click event.

   This handler needs to prompt the MediaPlayer to fire the `AdClicked` event. 

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   
   ```

1. Add event listeners for the MediaPlayer ad start, ad clicked, and ad completed notifications.

   ```

    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 

    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);

    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Add event handlers.
   a. Handle the ad start event.
      This could do anything, such as setting up UI for the user.
   
      ```   
      onAdStarted = function (event) { 
          if (clickAddButton && event && event.ad) { 
              var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
              if (adClick && adClick.isValid) { 
                  // Do some initial processing  
                  // when the ad starts, prior 
                  // to the user's click. 
              } 
          } 
      }
      ```

   b. Handle the ad clicked event.
      In this example, we obtain ad information from the event and open a new browser window using that information:    
   
      ```   
      onAdClickedEvent = function (event) { 
          if (event && event.ad) { 
              var adClick = event.adClick; 
              if (!(adClick && adClick.isValid)) { 
                  adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
              } 
              if (adClick && adClick.isValid) 
              { 
                  // Do something with the currently playing ad 
                  window.open(adClick.url); 
              } 
          } 
      }
      ```

   c. Handle the ad completed event.

      ```   
      onAdCompleted = function (event) { 
          if (clickAddButton) { 
              clickAddButton.setAttribute('hidden', 'true'); 
          } 
      }
      ```
