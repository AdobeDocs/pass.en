---
description: You can set up one lace to handle errors.
title: Set up error handling
exl-id: 9b83b47e-6d30-452b-87c3-1e3a139f2e69
---
# Set up error handling {#set-up-error-handling}

You can set up one lace to handle errors.

1. Implement an event callback function for `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK passes event information, such as a `MediaPlayerStatusChangeEvent` object.
1. In the callback, when the returned status is `MediaPlayerStatus.ERROR`, provide logic to handle all errors.
1. After the error is handled, reset the `MediaPlayer` object or load a new media resource.

   When the `MediaPlayer` object is in the error status it remains in that status until you reset it using the `MediaPlayer.reset` method.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

For example: 

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```
