---
description: Your application must use the appropriate TimedMetadata objects at the appropriate times.
title: Store timed metadata objects as they are dispatched
exl-id: da7ee636-f3ac-4aac-9ca0-7075b8c910f0
---
# Store timed metadata objects as they are dispatched {#store-timed-metadata-objects-as-they-are-dispatched}

Your application must use the appropriate TimedMetadata objects at the appropriate times.

 During content parsing, which happens before playback, TVSDK identifies subscribed tags and notifies your application about these tags.

>[!TIP]
>
>The time that is associated with each `TimedMetadata` is the local time on the playback timeline.

To store timed metadata objects as they are dispatched: 

1. Keep track of the current playback time.
1. Match the current playback time to the dispatched `TimedMetadata` objects.

1. Use the `TimedMetadata` where the start time equals the current local playback time.

   The following example shows how to save `TimedMetadata` objects in an `ArrayList`. 

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```
