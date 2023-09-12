---
description: You can handle blackouts in live video streams and provide alternate content during a blackout.
title: Blackout API elements
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
---
# Blackout API elements{#blackout-api-elements}

You can handle blackouts in live video streams and provide alternate content during a blackout.

When a blackout occurs in a live stream, your player uses event handlers to detect the blackout and provide alternate content to those users who are ineligible to watch the main stream. Your player detects the start and end of the blackout period, switches playback from the main stream to an alternate stream, and switches back to the main stream when the blackout period ends.

To handle blackouts in live streams:

1. Set up your app to detect blackout tags by subscribing to blackout tags in a live-stream manifest.

   TVSDK does not detect blackout tags on its own; you must subscribe to blackout tags to receive notification when the tags are encountered during manifest file parsing. 
1. Create event listeners for tags to which your player is subscribed  (in this case, PLAYBACK and BLACKOUTS tags) .

   When a tag occurs that your player has subscribed to (for example, a blackout tag) in either the foreground (main content) or background (alternate content) stream manifests, TVSDK dispatches a `TimedMetadataEvent` and creates a `TimedMetadataObject` for the `TimedMetadataEvent`. 

1. Implement handlers for the timed metadata events for both the foreground and the background streams.

   In these handlers, get the start and end times for the blackout period from the timed metadata event objects. 
1. Create methods for switching content at the start and end of the blackout period.

   When the blackout period starts, switch the main content to the background and switch the alternate content to become the main stream. Continue to fetch and parse the original manifest in the background and keep checking for the "blackout end" tag, so that the player can rejoin the original stream when the blackout ends. 
1. Update non seekable ranges if the blackout range is in DVR on the playback stream.

   Track and handle the `TimedMetadata` on the background stream, by preparing and updating blackout non seekable ranges.

TVSDK provides API elements that are useful when implementing blackouts, including methods, metadata, and notifications.

You can use the following when implementing a blackout solution in your player.

* **MediaPlayer**

    * `registerCurrentItemAsBackgroundItem` Saves the currently loaded resource as the background resource. If `replaceCurrentResource` is called after this method, TVSDK continues to download the background item's manifest until you call `unregisterCurrentBackgroundItem`, `release`, or `reset`. 
    
    * `unregisterCurrentBackgroundItem` Sets the background item to null and stops fetching and parsing the background manifest.

* **BlackoutMetadata** -

  A Metadata class that is specific to blackouts.

  This allows you to set non seekable ranges (an array of `TimeRanges`) on TVSDK. TVSDK checks for these ranges every time the user seeks. If it is set and the user seeks into a nonseekable range, TVSDK forces the viewer to the end of the nonseekable range. 

* **START HERE NEXT AdvertisingMetadata** Enable or disable preroll on a live stream by setting `enableLivePreroll` to true or false. If false, TVSDK does not make an explicit ad server call for pre-roll ads before the content playback and so does not play the pre-roll. This has no impact on the mid-rolls. The default is true. 

* **MediaPlayer.BlackoutsEventListener**

    * `onTimedMetadataInBackgroundItem` - Dispatched when detects a subscribed tag in the background manifest and a new `TimedMetadata` instance is prepared from it. The `TimedMetadata` instance is dispatched as a parameter. 
    
    * `onBackgroundManifestFailed` - Dispatched when the media player completely fails to load the background manifest, that is, all of the stream URLs return either an error or an invalid response.

* **Notifications**

    * `BACKGROUND_MANIFEST_WARNING`

        * Code: 204000 
        * Type: Warning 
        * Error in background manifest download.
