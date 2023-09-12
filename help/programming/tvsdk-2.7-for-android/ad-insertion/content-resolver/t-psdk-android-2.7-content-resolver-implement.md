---
description: You can implement your own content resolvers based on the default resolvers.
title: Implement a custom content resolver
exl-id: 04eff874-8a18-42f0-adb2-5b563e5c6a31
---
# Implement a custom content resolver {#implement-a-custom-content-resolver}

You can implement your own content resolvers based on the default resolvers.

When TVSDK generates a new opportunity, it iterates through the registered content resolvers looking for one that is capable of resolving that opportunity. The first one that returns `true` is selected to resolve the opportunity. If no content resolver is capable, that opportunity is skipped. Because the content resolving process is usually asynchronous, the content resolver is responsible for notifying TVSDK when the process has completed. 

1. Implement your own custom `ContentFactory`, by extending the `ContentFactory` interface and overriding `retrieveResolvers`.

   For example: 

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
    
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   
   ```

1. Register the `ContentFactory` to the `MediaPlayer`.

   For example: 

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
    
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
    
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Pass an `AdvertisingMetadata` object to TVSDK as follows:
   1. Create an `AdvertisingMetadata` object.
   1. Save the `AdvertisingMetadata` object to `MediaPlayerItemConfig`.

      ```java   
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
       
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
       
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      
      ```

1. Create a custom ad resolver class that extends the `ContentResolver` class.
   1. In the custom ad resolver, override `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java   
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      You get your `advertisingMetadata` from the item passed in `doConfigure`:    
   
      ```java   
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
       
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      
      ```

   1. For each placement opportunity, create a `List<TimelineOperation>`.
   
      This sample `TimelineOperation` provides a structure for `AdBreakPlacement`:    
   
      ```java   
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      
      ```

   1. After ads are resolved, call one of the following functions:

       * If the ad resolve succeeds, call `process(List<TimelineOperation> proposals)` and `notifyCompleted(Opportunity opportunity)` on the `ContentResolverClient`        
       
         ```java       
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         
         ```

       * If the ad resolve fails, call `notifyResolveError` on the `ContentResolverClient`        
       
         ```java       
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         For example:        
       
         ```java       
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

This sample custom ad resolver resolves an opportunity and serves a simple ad: 

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 

```
