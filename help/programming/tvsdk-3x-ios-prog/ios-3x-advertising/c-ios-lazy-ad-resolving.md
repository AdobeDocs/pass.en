---
description: Ad resolving and ad loading may cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading Resolving feature can reduce this startup delay. Ads can now be resolved at a specified interval prior to the position of the ad break. This is achieved by using a dual player approach.
title: Just-in-Time ad resolving
exl-id: dd5342c5-9f34-4778-a47a-91ff2eb03155
---
# Just-in-Time ad resolving {#just-in-time-ad-resolving}

Ad resolving and ad loading may cause an unacceptable delay for a user waiting for playback to start. The Lazy Ad Loading Resolving feature can reduce this startup delay. Ads can now be resolved at a specified interval prior to the position of the ad break. This is achieved by using a dual player approach.

**Basic ad resolving and loading process:**

  1. TVSDK downloads a manifest (playlist) and *resolves* all of the ads. 
  1. TVSDK *loads* all of the ads and stitches the ad segments into the manifests. 
  1. TVSDK moves the player into the PREPARED status, and content playback begins.

The player uses the URLs in the manifest to obtain the ad content (creatives), ensures that the ad content is in a format that TVSDK can play, and TVSDK places the ads on the timeline. This basic process of resolving and loading ads can cause an unacceptably long delay for a user waiting to play their content, especially if the manifest contains several ad URLs. 

**Lazy Ad Resolving:**

  1. TVSDK downloads the playlist. 
  1. TVSDK *resolves and loads* any pre-roll ads, moves the player into the PREPARED status, and content playback begins. 
  1. TVSDK *resolves* each ad breaks prior to its' position based on the value defined in `PTAdMetadata::delayAdLoadingTolerance`.

For instance, by default `delayAdLoadingTolerance` is set to 5 seconds. If an AdBreak is set to be played at 3:00, it will be resolved at 2:55:00. You may want to increase this value if you believe your ad resolution will take longer than 5 seconds.

>[!IMPORTANT]
>
>**Factors to consider with Lazy Ad Resolving:** 
>* Lazy Ad Resolving is only supported for VOD streams only with modes SERVER_MAP ad signaling mode. 
>* Lazy Ad Resolving is not enabled by default. You must set `PTAdMetadata::delayAdLoading` = YES to enable it. 
>* Lazy Ad Resolving is incompatible with the Instant On feature. For more information about Instant On, see [Instant On](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md). 
>* Picture-in-Picture mode is not supported with Lazy Ad Resolving. Please disable any Picture-in-picture modes if you enable Lazy Ad Resolving. 
>* Lazy ad resolution does not affect pre-roll ads. 
>
**Enable lazy ad resolving**

You can enable or disable the Lazy Ad Resolving feature using the existing Lazy Ad Loading mechanism (Lazy Ad Resolving is disabled by default).

You can enable Lazy Ad Resolving by setting `PTAdMetadata::delayAdLoading`= YES when setting up your ad metadata.

**APIs relevant to lazy ad resolution:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
