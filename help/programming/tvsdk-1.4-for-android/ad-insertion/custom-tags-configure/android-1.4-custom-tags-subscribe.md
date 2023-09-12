---
description: TVSDK prepares TimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.
title: Subscribe to custom tags
exl-id: 7f1f86ca-eeba-43c3-ac2a-c493d05ad73a
---
# Subscribe to custom tags{#subscribe-to-custom-tags}

TVSDK prepares TimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.

Before the playback starts, you must subscribe to the tags. 
To be notified about custom tags in HLS manifests: 

   Set the custom ad tag names globally by passing an array that contains the custom tags to `setSubscribedTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >You must include the `#` prefix when working with HLS streams.

   For example: 

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
