---
description: You can implement your own content resolvers based on the default resolvers.
title: Implement a custom content resolver
exl-id: 96468f6d-80ad-4721-8ed3-4dbfa2a64b9e
---
# Implement a custom content resolver {#implement-a-custom-content-resolver}

You can implement your own content resolvers based on the default resolvers.

When TVSDK detects a new opportunity, it iterates through the registered content resolvers looking for one that is capable of resolving that opportunity. The first one that returns true is selected for resolving the opportunity. If no content resolver is capable, then that opportunity is skipped. Because the content resolving process is usually asynchronous, the content resolver is responsible for notifying  when the process has completed.

1. Create a custom `AdvertisingFactory` instance and override `createContentResolver`.

   For example:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public ContentResolver createContentResolver(MediaPlayerItem item) { 
           Metadata metadata = _mediaPlayer.getCurrentItem().getResource().getMetadata(); 
           if (metadata != null) { 
               if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
                   return new AuditudeResolver(getActivity().getApplicationContext()); 
               } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
                   return new MetadataResolver(); 
               } else if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
                   return new CustomAdMarkersContentResolver(); 
               } else if (metadata.containsKey(CustomAdResolver.CUSTOM_METADATA_KEY)) { 
                   return new CustomAdResolver(); 
               } 
           } 
           return null; 
       } 
       ... 
   }
   ```

1. Register the ad client factory to the `MediaPlayer`.

   For example:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Pass an `AdvertisingMetadata` object to TVSDK as follows:
   1. Create an `AdvertisingMetadata` object and `MetadataNode` object.
   1. Save the `AdvertisingMetadata` object to `MetadataNode`.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. Create a custom ad resolver class that extends the `ContentResolver` class.
   1. In the custom ad resolver, override this protected function:

      ```java   
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```   
   
      Metadata contains your `AdvertisingMetada`. Use it for the following `TimelineOperation` vector generation. 
   
   1. For each placement opportunity, create a `Vector<TimelineOperation>`.
   
      The vector can be empty, but not null.

      This sample `TimelineOperation` provides a structure for `AdBreakPlacement`:    
   
      ```java   
      AdBreakPlacement(AdBreak.createAdBreak( 
                                ads,       // Vector<Ad> 
                                time,      // Ad Break start time. Note: local time on the timeline 
                                duration,  // Ad Break duration 
                                tag()      // An arbitrary string value that can be attached to  
                                           // the AdBreak object. 
                               ), placementInformation  // Retrieved from PlacementOpportunity 
      )
      ```   
   
   1. After ads are resolved, call one of the following functions:

       * If the ad resolve succeeds: `notifyResolveComplete(Vector<TimelineOperation> proposals)` 
       * If the ad resolve fails: `notifyResolveError(Error error)`

      For example, if it fails:    
   
      ```java   
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```

<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

This sample custom ad resolver makes an HTTP request to the ad server and receives a JSON response.

```java
public class CustomAdResolver extends ContentResolver { 
    ... 
    @Override 
    protected void doResolveAds(Metadata metadata, PlacementOpportunity placementOpportunity) { 
        ... 
        if (resolveSuccess == true) { 
            notifyResolveComplete(Vector<TimelineOperation> proposals); 
        } 
        else { 
            notifyResolveError(Error error); 
        } 
    } 
    ... 
}
```

Sample JSON ad server response for a live stream: 

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } 
        ] }, 
        { 
            "start": -1, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 

```

Sample JSON ad server response for VOD: 

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": {  
                } 
            }, 
            { 
                "id": 1002, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/crescent/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset2", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 50000, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 100000000, 
            "ads": [ { 
                "id": 1004, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/camry/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset4", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 

```
