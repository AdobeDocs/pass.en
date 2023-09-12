---
description: You can implement your own opportunity detectors.
title: Implement a custom opportunity detector
exl-id: a3f6d6b3-4d5e-49bc-b8de-a1196305bbb4
---
# Implement a custom opportunity detector{#implement-a-custom-opportunity-detector}

You can implement your own opportunity detectors.

* If your opportunity generator is based on `TimedMetadata` objects associated with the current media stream, then it should extend the `SpliceOutOpportunityGenerator` or `TimedMetadataOpportunityGenerator`. 

* If your opportunity generator is based on out-of-band data provided by an external service (such as a CIS), then it should extend the `OpportunityGenerator`.

1. Create the custom opportunity generator.

       If your custom opportunity generator is based on `TimedMetadata` objects, then extend the `TimedMetadataOpportunityGenerator` and override these methods:

    * `doConfigure` - This method is called after the media player item has been created and provides the opportunity generator to create an initial set of opportunities if needed 
    * `doProcess` - This method is called every time new `TimedMetadata` is detected (for example, for live/linear streams every time the playlist/manifest refreshes)

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
             
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
     
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
             
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. Create the custom content factory, which uses the custom opportunity generator.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
     
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
             
           return result; 
       } 
   }
   ```

1. Register the custom content factory for the media stream to be played.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
     
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
