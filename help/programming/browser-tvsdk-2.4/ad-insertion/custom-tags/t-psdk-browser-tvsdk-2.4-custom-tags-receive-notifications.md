---
description: To receive notifications about tags in the manifest, listen for AdobePSDK.TimedMetadataEvent.
title: Add listeners for timed-metadata notifications
exl-id: eea2505f-595c-4bbe-9b68-ae395943c888
---
# Add listeners for timed-metadata notifications{#add-listeners-for-timed-metadata-notifications}

To receive notifications about tags in the manifest, listen for AdobePSDK.TimedMetadataEvent.

When a new `TimedMetadata` object is created, the MediaPlayer dispatches `AdobePSDK.TimedMetadataEvent`. 

1. Implement the appropriate listeners.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   
   ```

1. Register the event listeners.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

ID3 metadata is dispatched through the same `Events.TimedMetadataEvent`. You can use the `timedMetadata.type` property to distinguish between TAG and ID3.
