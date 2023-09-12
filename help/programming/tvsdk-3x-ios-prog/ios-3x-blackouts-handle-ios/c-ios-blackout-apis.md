---
description: TVSDK provides API elements that are useful when implementing blackouts, including methods, metadata, and notifications.
title: Blackout API elements
exl-id: 76d99d8d-1aae-4faa-aaf2-bb7b535a1c71
---
# Blackout API elements {#blackout-api-elements}

TVSDK provides API elements that are useful when implementing blackouts, including methods, metadata, and notifications.

You can use the following when implementing a blackout solution in your player.

* **PTMediaPlayer**

    * `registerCurrentItemAsBackgroundItem` Saves the currently loaded resource as the background resource. If `replaceCurrentItemWithPlayerItem` is called after this method, TVSDK continues to download the background item's manifest until you call `unregisterCurrentBackgroundItem` , `stop`, or `reset` . 
    
    * `unregisterCurrentBackgroundItem` Sets the background item to nil and stops fetching and parsing the background manifest.

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` class that is specific to blackouts.

  This allows you to set nonseekable ranges (an array of `CMTimeRanges`) on TVSDK. TVSDK checks for these ranges every time the user seeks. If it is set and the user seeks into a nonseekable range, TVSDK forces the viewer to the end of the nonseekable range. 

* **START HERE NEXT** **PTAdMetadata** Enable or disable pre-roll on a live stream by setting `enableLivePreroll` to YES or NO. If NO, TVSDK does not make an explicit ad server call for pre-roll ads before the content playback and so does not play the pre-roll. This has no impact on the mid-rolls. The default is YES. 

* **NSNotifications**

    * `PTTimedMetadataChangedInBackgroundNotification` - Posted when TVSDK detects a subscribed tag in the background manifest and a new `PTTimedMetadata` instance is prepared from it. The notification's object is the `PTMediaPlayerItem` instance that is currently playing. You can fetch the `PTTimedMetadata` instance from the notification's `userInfo` dictionary using the `PTTimedMetadataKey` key. 
    
    * `PTBackgroundManifestErrorNotification` - Posted when the media player completely fails to load the background manifest, that is, all of the stream URLs return either an error or an invalid response. The notification's object is the `PTMediaPlayerItem` instance that is currently playing.

* **PTNotification**

    * `BACKGROUND_MANIFEST_WARNING`

        * Code: 204000 
        * Type: Warning 
        * Error in background manifest download.

    * `INVALID_SEEK_WARNING` Dispatched when a seek is attempted in a nonseekable range (in `nonSeekableRanges` set in `PTBlackoutMetadata`).
