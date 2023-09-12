---
description: You can implement your own opportunity detectors by implementing the interface PlacementOpportunityDetector.
title: Implement a custom opportunity detector
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
---
# Implement a custom opportunity detector {#implement-a-custom-opportunity-detector}

You can implement your own opportunity detectors by implementing the interface PlacementOpportunityDetector.

1. Create a custom `AdvertisingFactory` instance and override `createOpportunityDetector`. For example:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. Register the ad client factory to the `MediaPlayer`. For example:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Create a custom opportunity detector class that extends the `PlacementOpportunityDetector` class.
   1. In the custom opportunity detector, override this function:

      ```java   
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```   
   
      The `timedMetadataList` contains the list of available `TimedMetadata`, which is sorted. Metadata contains the targeting parameters and the custom parameters to be sent to the ad provider. 
   
   1. For each `TimedMetadata`, create a `List<PlacementOpportunity>`. The list can be empty, but not null. `PlacementOpportunity` should have the following attributes:

      ```java   
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. After placement opportunities are created for all the detected timed metadata objects, simply return the `PlacementOpportunity` list.

This is a sample custom placement opportunity detector:

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 

```
