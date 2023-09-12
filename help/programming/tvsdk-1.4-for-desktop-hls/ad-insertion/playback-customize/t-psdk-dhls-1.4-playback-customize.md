---
description: You can customize or override ad behaviors.
title: Set up customized playback
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
---
# Set up customized playback{#set-up-customized-playback}

You can customize or override ad behaviors.

Before you can customize or override ad behaviors, register the ad policy instance with . 
To customize ad behaviors, do one of the following:

* Implement the `AdPolicySelector` interface and all its methods.

  This option is recommended if you need to override **all** the default ad behaviors. 

* Extend the `DefaultAdPolicySelector` class and provide implementations for only those behaviors that require customization.

  This option is recommended if you need to override only **some** of the default behaviors.

For both options, complete the following tasks: 

1. Implement your own custom ad policy selector.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Extend the content factory to use the custom ad policy selector.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. Register the new content factory to be used by TVSDK in the advertising workflow.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >If the custom content factory was registered for a specific stream through the `MediaPlayerItemConfig` class, it will be cleared when the `MediaPlayer` instance is deallocated. Your application must register it each time a new playback session is created.
