---
description: You can override the default behavior for how TVSDK seeks over ads when using custom ad markers.
title: Control playback behavior for seeking over custom ad markers
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
---
# Control playback behavior for seeking over custom ad markers{#control-playback-behavior-for-seeking-over-custom-ad-markers}

You can override the default behavior for how TVSDK seeks over ads when using custom ad markers.

By default, when a user seeks into or past ad sections that result from the placement of custom ad markers, TVSDK skips the ads. This might differ from the current playback behavior for standard ad breaks.

You can tell TVSDK to reposition the playhead to the beginning of the most recently skipped custom ad when the user seeks past one or more custom ads. 

1. Configure a Metadata instance with the `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumeration set to the string value "true" (not as a Boolean `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Create and configure a `MediaResource` instance, passing the additional configuration options to `TimeRangeCollection.toMetadata`. This method receives additional configuration options via another generic metadata structure.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
