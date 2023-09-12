---
description: You can handle blackouts in live video streams and provide alternate content during a blackout.
title: Handle blackouts in live streams
exl-id: 2e63fb0c-44b1-46f1-a4b8-f8f67389d183
---
# Handle blackouts in live streams{#handle-blackouts-in-live-streams}

You can handle blackouts in live video streams and provide alternate content during a blackout.

When a blackout occurs in a live stream, your player uses event handlers to detect the blackout and provide alternate content to those users who are ineligible to watch the main stream. Your player detects the start and end of the blackout period, switches playback from the main stream to an alternate stream, and switches back to the main stream when the blackout period ends.

In your client app, you subscribe for blackout tags in TVSDK. Upon being notified of new *timed metadata* objects, you parse the timed metadata object's data to identify whether the object indicates a blackout entry or exit. For identified blackouts, you call the relevant TVSDK elements to switch to alternate content at the beginning of the blackout, and again to return to the main content when the blackout is over.

>[!TIP]
>
>The keys are still downloaded from manifest before the content is played.

When a user connects to a live stream after the blackout period is over, and scrolls back in time to the blacked-out period, the content will play. 

>[!IMPORTANT]
>
>If all of the key requests fail, an error is thrown when parsing the manifest. If some requests fail and some succeed, TVSDK attempts to play the content. If TVSDK attempts to play a section of the content, but there is no valid key to decrypt this content, it returns an error.

To handle blackouts in live streams:

1. Set up your app to detect blackout tags by subscribing to blackout tags in a live-stream manifest.

   TVSDK does not detect blackout tags on its own; you must subscribe to blackout tags to receive notification when the tags are encountered during manifest file parsing. 
1. Create event listeners for tags to which your player is subscribed.

   When a tag occurs that your player has subscribed to (for example, a blackout tag) in either the foreground (main content) or background (alternate content) stream manifests, TVSDK dispatches a `TimedMetadataEvent` and creates a `TimedMetadataObject` for the `TimedMetadataEvent`. 
1. Implement handlers for the timed metadata events for both the foreground and the background streams.

   In these handlers, get the start and end times for the blackout period from the timed metadata event objects. 
1. Prepare the `MediaPlayer` for blackouts.

   When the `MediaPlayer` enters the PREPARED state, you calculate and prepare the blackout ranges and set them on the `MediaPlayer` objtect. 

1. For each update to the playhead position, check the list of `TimedMetadataObjects`.

   This is where your player detects the blackout start and end, and tracks the time of the blackout as it occurs. 

1. Create methods for switching content at the start and end of the blackout period.

   When the blackout period starts, switch the main content to the background and switch the alternate content to become the main stream. Continue to fetch and parse the original manifest in the background and keep checking for the "blackout end" tag, so that the player can rejoin the original stream when the blackout ends.
