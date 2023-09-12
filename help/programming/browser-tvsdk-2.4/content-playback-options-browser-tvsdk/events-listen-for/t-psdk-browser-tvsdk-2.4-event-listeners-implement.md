---
description: Event handlers allow Browser TVSDK to respond to events.
title: Implement event listeners and callbacks
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
---
# Implement event listeners and callbacks{#implement-event-listeners-and-callbacks}

Event handlers allow Browser TVSDK to respond to events.

When an event occurs, Browser TVSDK's event mechanism calls your registered event handler and passes the event information to the handler.

Your application must implement event listeners for Browser TVSDK events that affect your application. 

1. Determine for which events your application must listen.

    * **Required events**: Listen for all playback events.     
    
      >[!IMPORTANT]
      >
      >The playback event `STATUS_CHANGED` provides the player state, including errors. Any of the states might affect your player's next step.

    * **Other events**: Optional, depending on your application.

      For example, if you incorporate advertising in your playback, listen for all `AdBreakPlaybackEvent` and `AdPlaybackEvent` events.

1. Implement event listeners for each event.

   Browser TVSDK returns parameter values to your event-listener callbacks. These values, provide relevant information about the event that you can use in your  listeners  to perform appropriate actions.

   For example:

   * Event type: `AdobePSDK.PSDKEventType.STATUS_CHANGED` 
   * Event property: `MediaPlayerStatus.<event>` used like this: 

  ```js
  player.addEventListener( 
              AdobePSDK.PSDKEventType.STATUS_CHANGED,  
              onStatusChange); 
   
  onStatusChange = function (event) { 
   
      switch (event.status) { 
          case AdobePSDK.MediaPlayerStatus.IDLE: 
              console.log("Player Status: IDLE"); 
              break;
  ```

1. Register your callback  listeners  with the `MediaPlayer` object  by using `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
