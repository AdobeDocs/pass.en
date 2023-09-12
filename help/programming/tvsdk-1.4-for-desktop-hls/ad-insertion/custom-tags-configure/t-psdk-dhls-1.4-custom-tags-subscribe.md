---
description: TVSDK prepares TimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.
title: Subscribe to custom tags
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
---
# Subscribe to custom tags{#subscribe-to-custom-tags}

TVSDK prepares TimedMetadata objects for subscribed tags each time these objects are encountered in the content manifest.

Before the playback starts, you must subscribe to the tags. 
To subscribe to tags, assign a vector that contains the custom tag names to the `subscribedTags` property. If you need to also change the ad tags used by the default opportunity generator, then assign a vector that contains the custom ad tag names to the `adTags` property.

To be notified about custom tags in HLS manifests: 

1. Set the custom ad tag names globally by assigning a vector that contains the custom tags to `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >You must include the `#` prefix when working with HLS streams.

   For example: 

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. To globally change the ad tags that are used by the default opportunity generator, assign a vector that contains the custom ad tag names to the `adTags` property in `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   
   ```

1. To have all the global settings take effect, replace the current resource.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. To set the subscribed tag names for a stream, if needed:
   1. Create a media player item configuration.

      >[!TIP]
      >
      >The easiest way is to create a default media player item configuration.

   1. Assign a vector that contains the custom tags to `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
            
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. To change the ad tags that are used by the default opportunity generator in the specified stream, assign a vector that contains the custom ad tag names to the `adTags` property in `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. To have the changes for the stream take effect, when loading the media stream, use the media player item configuration.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
