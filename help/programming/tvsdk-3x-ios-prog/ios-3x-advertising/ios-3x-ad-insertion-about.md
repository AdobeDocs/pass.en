---
description: Ad insertion resolves ads for video-on-demand (VOD) , for live streaming, and for linear streaming with ad tracking and ad playback. TVSDK makes the required requests to the ad server, receives information about ads for the specified content, and places the ads in the content in phases.
title: Insert ads
exl-id: 94262bd5-3f8c-449d-934f-8177869707bc
---
# Insert ads {#insert-ads}

Ad insertion resolves ads for video-on-demand (VOD) , for live streaming, and for linear streaming with ad tracking and ad playback. TVSDK makes the required requests to the ad server, receives information about ads for the specified content, and places the ads in the content in phases.

An *`ad break`* contains one or more ads that play in sequence. TVSDK inserts ads in the main content as members of one or more ad breaks.

>[!TIP]
>
>If the ad has errors, TVSDK ignores the ad.

## Resolve and insert VOD ads {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK supports several use cases for VOD ad resolving and insertion.

* Pre-roll ad insertion, where ads are inserted at the beginning of the content. 
* Mid-roll ad insertion, where at least one ad is inserted in the middle of the content. 
* Post-roll ad insertion, where at least one ad is appended at the end of the content.

TVSDK resolves the ads, inserts the ads in locations defined by the ad server, and computes the virtual timeline before playback starts. After playback starts, no changes, such as ads being inserted or inserted ads being removed, can occur.

## Resolve and insert live and linear ad {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK supports several use cases for live and linear ad resolving and insertion.

* Pre-roll ad insertion, where at least one ad is inserted at the beginning of the content. 
* Mid-roll ad insertion, where at least one ad is inserted in the middle of the content.

TVSDK resolves the ads and inserts the ads when a cue point is encountered in the live or linear stream. By default, TVSDK supports the following cues as valid ad markers when resolving and placing ads:

* #EXT-X-CUEPOINT 
* #EXT-X-AD 
* #EXT-X-CUE 
* #EXT-X-CUE-OUT

These markers require the metadata field's `DURATION` in seconds and the cue's unique ID. For example: 

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 

```

For more information about additional cues, see [Subscribe to custom tags](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md).

## Track client ad {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK automatically tracks ads for VOD and live/linear streaming.

Notifications are used to inform your application about an ad's progress, including information about when an ad begins and when it ends.

## Implement an early ad break return {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

For live stream ad insertion, you might need to exit from an ad break before all the ads in the break are played to completion.

Here are some examples for an early ad break return:

* The duration of the ad break in certain sports events.

  Although a default duration is provided, if the game resumes before the break finishes, the ad break must be exited. 
* An emergency signal during an ad break in a live stream.

The ability to exit from an ad break early is identified through a custom tag in the manifest known as a splice-in or a cue-in tag. TVSDK allows the application to subscribe to these splice-in tags to provide a splice-in opportunity.

* To use the `#EXT-X-CUE-IN` tag as a splice-in opportunity and implement an early ad break return:

    1. Subscribe to the tag.

       ```    
       [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
       ```

    1. Add the cue-in opportunity resolver.

       ```    
       // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
       // Set cue in opportunity resolver 
       [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
       ```

* To share the same tag for splice-out and splice-in:

1. If the application is sharing the same cue to indicate cue-out/splice-out and cue-in/splice-in, extend `PTDefaultAdOpportunityResolver` and implement the `preparePlacementOpportunity` method.     

   >[!TIP]
   >
   >The following code assumes that the app has an implementation for the `isCueInOpportunity` method. 

   ```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
   ```

1. Register the extended opportunity resolver on the `PTDefaultMediaPlayerClientFactory` instance.

```  
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
