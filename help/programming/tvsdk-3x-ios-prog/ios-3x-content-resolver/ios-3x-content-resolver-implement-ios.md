---
description: You can implement your resolvers based on the default resolvers.
title: Implement a custom opportunity/content resolver
exl-id: a73f62e1-7e6e-4b16-9bf8-118ec0381c41
---
# Implement a custom opportunity/content resolver {#implement-a-custom-opportunity-content-resolver}

You can implement your resolvers based on the default resolvers.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Develop a custom ad resolver by extending the `PTContentResolver` abstract class.

   `PTContentResolver` is an interface that must be implemented by a content resolver class. An abstract class with the same name is also available and handles the configuration automatically (getting the delegate). 

   >[!TIP]
   >
   >`PTContentResolver` is exposed through the `PTDefaultMediaPlayerClientFactory` class. Clients can register a new content resolver by extending the `PTContentResolver` abstract class. By default, and unless specifically removed, a `PTDefaultAdContentResolver` is registered in the `PTDefaultMediaPlayerClientFactory`.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
     
   @interface PTContentResolver : NSObject <PTContentResolver> 
     
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
     
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. Implement `shouldResolveOpportunity` and return `YES` if it should handle the received `PTPlacementOpportunity`.
1. Implement `resolvePlacementOpportunity`, which starts loading the alternate content or ads.
1. After the ads are loaded, prepare a `PTTimeline` with the information about the content to insert.

       Here is some useful information about timelines:

    * There can be multiple `PTAdBreak`s of pre-roll, mid-roll, and post-roll types.

        * A `PTAdBreak` has the following:

            * A `CMTimeRange` with the start time and duration of the break.

              This is set as the range property of `PTAdBreak`. 
            
            * `NSArray` of `PTAd`s.

              This is set as the ads property of `PTAdBreak`.

    * A `PTAd` represents the ad, and each `PTAd` has the following:

        * A `PTAdHLSAsset` set as the primary asset property of the ad. 
        * Possibly multiple `PTAdAsset` instances as clickable ads or banner ads.

   For example: 

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
      
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
      
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
      
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
      
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
      
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. Call `didFinishResolvingPlacementOpportunity`, which provides the `PTTimeline`.
1. Register your custom content/ad resolver to the default media player factory by calling `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
     
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
     
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. If you implemented a custom opportunity resolver, register it to the default media player factory.

   >[!TIP]
   >
   >You do not have to register a custom opportunity resolver to register a custom content/ad resolver.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
     
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
     
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

When the player loads the content, and it is determined to be of type VOD or LIVE, one of the following occurs:

* If the content is VOD, the custom content resolver is used to get the ad timeline of the entire video. 
* If the content is LIVE, the custom content resolver is called each time a placement opportunity (cue point) is detected in the content.
