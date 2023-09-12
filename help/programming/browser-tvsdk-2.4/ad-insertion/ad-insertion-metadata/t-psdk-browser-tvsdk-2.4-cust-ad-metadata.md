---
description: You can customize ad insertion metadata.
title: Customize ad insertion metadata
exl-id: 4881ace6-e97b-448d-8fb4-64e7b69517f1
---
# Customize ad insertion metadata{#customize-ad-insertion-metadata}

You can customize ad insertion metadata.

1. Set a timeout on advertising metadata for unresolved opportunities.

   The default value for this timeout is 20 seconds.
1. To change the value to 10 seconds, enter the following:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   The `timeout` property is defined in the `AdvertisingMetadata` class, and this timeout can be set for any custom ad settings that derives from the `AdvertisingMetadata` class. For example, if users define custom settings for a FreeWheel resolver, they can set a default timeout by using this setting. 

1. Create `MediaPlayerItemConfig` with the ad settings in step 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Use this configuration when calling `replaceCurrentResource` on `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
