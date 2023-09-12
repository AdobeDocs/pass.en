---
title: Mark ranges
description: Mark ranges
copied-description: yes
exl-id: b3314ee5-bb30-4b25-beff-ff810eff06b2
---
# Use cases to delete and replace ads {#use-cases-delete-replace-ads}

Here are the use cases to delete and replace ads:

## Mark ranges {#mark-ranges}

 To implement the `PTTimeRangeCollection` and mark ranges of content as ads: 
1. Prepare the `PTTimeRangeCollection`.
1. Set the type of the `PTTimeRangeCollection` to `PTTimeRangeCollectionTypeMarkRanges`.

   This step notifies TVSDK that the custom ranges must be treated like ads.

   ```
   #define PSDK_TIMESCALE 100000 
         
   NSArray *ranges =  @[ 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange  
       replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
         (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
         
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
       type:PTTimeRangeCollectionTypeMarkRanges];
   ```

1. Create the `PTAdMetadata` and set the `PTTimeRangeCollection`.

   ```
   // Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
     
   // Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
     
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
     
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

1. Create the player and start playback.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
     
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
     
   //Start playback 
   [player play];
   ```

## Replace ranges {#replace-ranges}

 To implement the `PTTimeRangeCollection` and delete ranges of content as ads: 
1. Prepare `PTTimeRangeCollection`.
1. Set the type of the `PTTimeRangeCollection` to `PTTimeRangeCollectionTypeReplaceRanges`.

   This step notifies TVSDK that the provided ranges need to be replaced with alternate content (ads).

   ```
   #define PSDK_TIMESCALE 100000 
         
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))  
       replacementDuration:CMTimeMakeWithSeconds(30, AD_TIMESCALE)] 
                       ]; 
         
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeReplaceRanges];
   ```

   >[!TIP]
   >
   >The argument `replacementDuration` is optional. If it is not defined, the `AdServer` determines the duration of the ad break.

1. Create the `PTAdMetadata` and set the `PTTimeRangeCollection`.

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
     
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeCustomRanges; 
     
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
     
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >Although the `signalingMode` is set as `PTAdSignalingModeCustomRanges`, this ad signaling mode is set automatically when setting the `PTTimeRangeCollection` of type `PTTimeRangeCollectionTypeReplace`.

1. Create the player and start playback.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
     
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
     
   //Start playback 
   [player play];
   ```

## Delete ranges {#delete-ranges}

 To implement the `PTTimeRangeCollection` and delete ranges of content as ads: 
1. Prepare the `PTTimeRangeCollection`.
1. Set the type of the `PTTimeRangeCollection` to `PTTimeRangeCollectionTypeDeleteRanges`, which notifies TVSDK that the provided ranges need to be deleted.

   ```
   #define PSDK_TIMESCALE 100000 
         
   NSArray *ranges =  @[ 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (0, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))], 
     [PTReplacementRange replacementRangeWithRange:CMTimeRangeMake(CMTimeMakeWithSeconds 
       (120, PSDK_TIMESCALE),CMTimeMakeWithSeconds(60, AD_TIMESCALE))] 
   ]; 
         
   PTTimeRangeCollection *timeRangeCollection =  
     [[PTTimeRangeCollection alloc] initWithRanges:ranges  
                                              type:PTTimeRangeCollectionTypeDeleteRanges];
   ```

1. Create the `PTAdMetadata` and set the `PTTimeRangeCollection`.

   ```
   //Create the PTPlayerItem metadata 
   PTMetadata *metadata = [[PTMetadata alloc] init]; 
     
   //Create the Ad metadata 
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init]; 
   adMetadata.timeRangeCollection = timerangeCollection; 
   adMetadata.zoneId = adZoneId; 
   adMetadata.domain = adDomain; 
   adMetadata.signalingMode = PTAdSignalingModeServerMap; 
     
   //Set Ad metadata 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
     
   //Create PTMediaPlayerItem 
   PTMediaPlayerItem *playerItem = [[[PTMediaPlayerItem alloc] initWithUrl:mediaUrl 
                                                                   mediaId:mediaId 
                                                                  metadata:metadata];
   ```

   >[!TIP]
   >
   >Ad insertion occurs after the deletion of the custom ranges based on the `PTAdMetadata` and the current `PTAdSignalingMode`.

1. Create the player and start playback.

   ```
   //Create PTMediaPlayer using the created PTMediaPlayer 
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:playerItem]; 
     
   //Add player to the player UIView 
   [self.playerView addSubview:(UIView *)player.view]; 
     
   //Start playback 
   [player play];
   ```
