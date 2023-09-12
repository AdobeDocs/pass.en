---
description: You can set up one place in your application to perform error handling in response to the ERROR state.
title: Set up error handling
exl-id: c0ce1d80-85d5-4344-9ab0-bd56906421cb
---
# Set up error handling{#set-up-error-handling}

You can set up one place in your application to perform error handling in response to the ERROR state.

1. Add an event listener for `AdobePSDK.MediaPlayerStatusChangeEvent`.

   For example: 

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. In your event listener, when the `event.status` is `AdobePSDK.MediaPlayerStatus.ERROR`, provide the logic to handle all errors.
1. After the error is handled, reset the `MediaPlayer` object or load a new media resource.

       When the MediaPlayer object is in the ERROR state, it cannot exit this state until you complete one of the following tasks:

    * Reset the MediaPlayer object by using the `MediaPlayer.reset` method. 
    * Load a new media resource by using the `MediaPlayer.replaceCurrentResource` method.

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

For example: 

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 

```
