---
description: TVSDK handles blackouts in live video streams and provides alternate content during a blackout.
title: Handle blackouts in live streams
exl-id: 772700ac-2b6d-4bf9-9400-c357dd77f701
---
# Handle blackouts in live streams{#handle-blackouts-in-live-streams}

TVSDK handles blackouts in live video streams and provides alternate content during a blackout.

The most common use case associated with a programming blackout is when your player app provides alternate content to users who are ineligible to watch the main stream. This app can use TVSDK to determine the beginning and the end of the blackout period. This way, at the beginning of the blackout period, playback can switch from the main stream to an alternate stream and then switch back to the main stream when the blackout period is over.

To implement the solution for this use case:

1. Set up your app to subscribe to blackout tags in a live stream manifest.

   TVSDK is not directly aware of blackout tags, but it allows your app to subscribe to notifications when specific tags are encountered during manifest file parsing. 
1. Add a notification listener for `PTTimedMetadataChangedNotification`.

   This notification is dispatched each time a subscribed tag is parsed in the manifest, and a new `PTTimedMetadata` is prepared from it. 

1. Implement a listener method, such as `onMediaPlayerSubscribedTagIdentified`, for `PTTimedMetadata` objects in foreground. 

1. Each time there is an update during playback, use the `PTMediaPlayerTimeChangeNotification` listener to handle `PTTimedMetadata` objects. 

1. Add the `PTTimedMetadata` handler.

   This handler allows you to switch to alternate content and return to the main content as indicated by the `PTTimedMetadata` object and its playback time. 

1. Use `onSubscribedTagInBackground` to implement the listener method for `PTTimedMetadata` objects in the background.

   This method monitors the timing on the background stream, which helps you determine when you can switch from alternate content back to the main content. 

1. Implement a listener method for background errors. 
1. If the blackout range is in the DVR on the playback stream, update the nonseekable ranges.

   Your application must set the nonseekable range in the DVR in the following cases:

    * When joining the main stream when a blackout is in the DVR. 
    * When switching back to the main content from the alternate content.
