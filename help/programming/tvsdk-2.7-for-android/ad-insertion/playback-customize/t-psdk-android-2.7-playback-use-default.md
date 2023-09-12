---
description: You can choose to use default ad behaviors.
title: Use the default playback behavior
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
---
# Use the default playback behavior  {#use-the-default-playback-behavior}

You can choose to use default ad behaviors.

1. To use default behaviors, complete one of the following tasks:

    * If you implement your own `AdvertisingFactory` class, return null for `createAdPolicySelector`. 
    
    * If you do not have a custom implementation for the `AdvertisingFactory` class, TVSDK uses a default ad policy selector.

## Set up customized playback {#set-up-customized-playback}

You can customize or override ad behaviors.

Before you customize or override ad behaviors, register the ad policy instance with TVSDK.

* Implement the `AdPolicySelector` interface and all its methods.

  This option is recommended if you need to override **all** the default ad behaviors. 

* Extend the `DefaultAdPolicySelector` class and provide implementations for only those behaviors that require customization.

  This option is recommended if you need to override only **some** of the default behaviors.

To customize ad behaviors: 

1. Implement the `AdPolicySelector` interface and all of its methods.
1. Assign the policy instance to be used by TVSDK through the advertising factory.

   >[!NOTE]
   >
   >Custom ad policies that are registered at the beginning of playback are cleared when the `MediaPlayer` instance is deallocated. Your application must register a policy selector instance each time a new playback session is created.

   For example: 

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
    
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
    
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. Implement your customizations.
