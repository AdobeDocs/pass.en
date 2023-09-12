---
description: You can override the default behavior for how TVSDK handles seeks over ads when using custom ad markers.
title: Control playback behavior for seeking over custom ad markers
exl-id: c148aca6-699d-4b93-9013-9e20bc391687
---
# Control playback behavior for seeking over custom ad markers {#control-playback-behavior-for-seeking-over-custom-ad-markers}

You can override the default behavior for how TVSDK handles seeks over ads when using custom ad markers.

By default, when a user seeks into or past ad sections that result from the placement of custom ad markers, TVSDK skips the ads. This might differ from the current playback behavior for standard ad breaks. You can set TVSDK to reposition the playhead to the beginning of the most recently skipped custom ad when the user seeks past one or more custom ads.

1. Call `CustomRangeMetadata.setAdjustSeekPosition` with `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Use `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
    
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   
   ```
