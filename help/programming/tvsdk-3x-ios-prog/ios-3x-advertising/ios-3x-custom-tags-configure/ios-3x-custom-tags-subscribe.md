---
description: TVSDK prepares PTTimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.
title: Subscribe to custom tags
exl-id: 5074e622-8824-4253-a668-485e2f68f156
---
# Subscribe to custom tags {#subscribe-to-custom-tags}

TVSDK prepares PTTimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.

Before the playback starts, you must subscribe to the tags. 
To be notified about custom tags in HLS manifests: 

1. Set the custom ad tag names globally by passing an array that contains the custom tags to `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >You must include the `#` prefix when working with HLS streams.

   For example: 

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
