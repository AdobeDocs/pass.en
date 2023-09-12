---
description: Set up a single place to handle errors.
title: Set up error handling
exl-id: ce4a2954-0166-43af-afdf-0aa24659f1ae
---
# Set up error handling{#set-up-error-handling}

Set up a single place to handle errors.

1. Implement an event callback function for `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK passes event information, such as a `MediaPlayerStatusChangeEvent` object.
1. In the callback, when the status from the event parameter is `MediaPlayerStatus.ERROR`, provide logic to handle all errors.
1. After the error is handled, reset the `MediaPlayer` object or load a new media resource.

   When the `MediaPlayer` object is in the ERROR state, it cannot exit this state until you either reset the `MediaPlayer` object (via the `MediaPlayer.reset` method) or load a new media resource ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

For example: 

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 

```
