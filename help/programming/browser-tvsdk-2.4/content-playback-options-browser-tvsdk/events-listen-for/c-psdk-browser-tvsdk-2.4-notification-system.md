---
description: The notification portion of the Browser TVSDK library allows you to create a logging and debugging system that can be useful for diagnostic and validation purposes.
title: Notification system
exl-id: 6a3a3c56-1580-4f43-ba81-220a5b0fe5c3
---
# Notification system {#notification-system}

The notification portion of the Browser TVSDK library allows you to create a logging and debugging system that can be useful for diagnostic and validation purposes.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Browser TVSDK has a *no throw* policy for its API. Most methods return an `PSDKErrorCode` value to indicate whether the method was executed successfully. For a complete list of all possible `PSDKErrorCode` values, see Browser TVSDK API references.

Asynchronous errors are notified through the specific events.

Browser TVSDK dispatches `MediaPlayer` events to provide information about player activity. You must implement event listeners to capture and respond to these events.

>[!TIP]
>
>Key events and information are logged on the web browser console.

## Listen for notifications {#section_06B96633433D497E842FB7ADD5F2C7DA}

You can listen for notifications and add your own notifications to the notification history. The core of the Browser TVSDK notification system is the `Notification` class, which represents a stand-alone notification.

To set up your application to listen for notifications:

1. Listen for MediaPlayer status changes by using the MediaPlayer instance. 

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implement the callback.

   The callback receives an instance of the `AdobePSDK.MediaPlayerStatusChangeEvent`, and Browser TVSDK passes this event object to the callback that contains the new player state. 
1. Your application can listen to other events that are dispatched by Browser TVSDK by using the `MediaPlayer` instance.
