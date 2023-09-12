---
description: You can implement your own content resolvers based on the default resolvers.
title: Implement a custom content resolver
exl-id: f594840b-ff56-49c5-baf5-ac2800411215
---
# Implement a custom content resolver{#implement-a-custom-content-resolver}

You can implement your own content resolvers based on the default resolvers.

 When Browser TVSDK detects a new opportunity, it iterates through the registered content resolvers looking for one that is capable of resolving that opportunity by using the `canResolve` method. The first one that returns true is selected for resolving the opportunity. If no content resolver is capable, then that opportunity is skipped. Because the content resolving process is usually asynchronous, the content resolver is responsible for notifying Browser TVSDK when the process has completed.

Remember the following information:

* The content resolver calls `client.process` to specify which timeline operation that TVSDK needs to execute.

  The operation is usually an ad break placement. 

* The content resolver calls `client.notifyCompleted` if the resolving process is succcessful or `client.notifyFailed` if the process fails.

1. Create a custom opportunity resolver.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
    
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
    
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
         
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
      
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
     
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
                 
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
     
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
    
   }; 
   
   ```

1. Create the custom content factory, which uses the custom content resolver.

   For example: 

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
    
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   
   ```

1. Register the custom content factory for the media stream to be played.

   In the UI Framework player, you can specify custom content factory as follows: 

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
    
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
    
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
    
   }); 
   
   ```
