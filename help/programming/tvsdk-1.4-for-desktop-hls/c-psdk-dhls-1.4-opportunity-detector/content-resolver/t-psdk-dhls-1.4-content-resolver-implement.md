---
description: You can implement your own content resolvers based on the default resolvers.
title: Implement a custom content resolver
exl-id: abe967a5-ced3-4e23-8671-065e256974d3
---
# Implement a custom content resolver{#implement-a-custom-content-resolver}

You can implement your own content resolvers based on the default resolvers.

 When TVSDK detects a new opportunity, it iterates through the registered content resolvers looking for one that is capable of resolving that opportunity  using the `canResolve` method . The first one that returns true is selected for resolving the opportunity. If no content resolver is capable, then that opportunity is skipped. Because the content resolving process is usually asynchronous, the content resolver is responsible for notifying TVSDK when the process has completed.

* The content resolver calls `client.place` to specify what timeline operation TVSDK needs to execute (usually an ad break placement). 
* The content resolver calls `client.notifyCompleted` if the resolving process is succcessful, or `client.notifyFailed` if the process fails.

1. Create a custom opportunity resolver.

   ```
   public class CustomResolver extends ContentResolver { 
     
       /** 
        * Default constructor. 
        */ 
       public function CustomResolver() { 
       } 
     
       override protected function doConfigure(item:MediaPlayerItem):void { 
           // here you can read any media stream characteristics which 
           // might help configure your content resolver like 
           // - the media player item configuration through the item.config 
           // - the media resource metadata through item.resource.metadata 
       } 
     
       /** 
        * @inheritDoc 
        */ 
       override protected function doCanResolve(opportunity:Opportunity):Boolean { 
           // check if the opportunity can be resolved by this resolver 
           // if yes return true, otherwise return false 
             
           return true; 
       } 
     
       /** 
        * @inheritDoc 
        */ 
       override protected function doResolve(opportunity:Opportunity):void { 
           // start the resolving process 
           // communicate with your custom ad server 
     
           // in this example we assume that: 
           // - if successful, onResolveCompleted method will be invoked 
           // - if failed, onResolveFailed method will be invoked 
       } 
     
       private function onResolveCompleted(response:*):void { 
           try { 
               var proposals:Vector.<TimelineOperation> = new Vector.<TimelineOperation>(); 
                 
               // extract the timeline ad placement from the response 
               // and add them to the proposal vector 
               // - extract the ad break 
               // - calculate the placement ( can reuse the opportunity.placement ) 
               // var timelineOperation:AdBreakPlacement = new AdBreakPlacement(placement, adBreak); 
               // proposals.push(timelineOperation); 
                 
               client.process(proposals); 
               client.notifyCompleted(_opportunity); 
           } catch (error:Error) { 
               onResolveFailed(error); 
           } 
       } 
     
       private function onResolveFailed(error:Error):void { 
     
           var errorMetadata:Metadata = new Metadata(); 
           MetadataUtils.serializeError(error, errorMetadata); 
     
           var mediaError:MediaError = new MediaError(NotificationCode.CONTENT_RESOLVING_ERROR, errorMetadata); 
           client.notifyFailed(_opportunity, mediaError); 
       } 
         
       ... 
   }
   ```

1. Create the custom content factory, which uses the custom content resolver.

   For example:

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
           ... 
     
           /** 
            * @inheritDoc 
            */ 
           override protected function  
             doRetrieveResolvers(item:MediaPlayerItem):Vector.<ContentResolver> { 
               var result:Vector.<ContentResolver> = new Vector.<ContentResolver>(); 
     
               var resource:MediaResource = item.resource; 
     
               if (resource.metadata != null) { 
                   if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
                       result.push(new AuditudeAdResolver()); 
                   } else if (resource.metadata.containsKey("custom-opportunity-detector")) { 
                       result.push(new CustomResolver()); 
                   } 
               } 
               return result; 
           } 
   }
   ```

1. Register the custom content factory for the media stream to be played.

   For example:

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
     
   var advertisingMetadata:AdvertisingMetadata = new AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue("customparam", "customvalue"); 
     
   var metadata:Metadata = new Metadata(); 
   metadata.setMetadata("custom-opportunity-detector", advertisingMetadata); 
   var mediaResource:MediaResource = MediaResource.createFromUrl(url, metadata);

   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
