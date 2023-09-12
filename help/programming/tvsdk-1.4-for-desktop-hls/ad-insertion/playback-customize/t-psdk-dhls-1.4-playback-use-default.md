---
description: You can choose to use default ad behaviors.
title: Use the default playback behavior
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
---
# Use the default playback behavior{#use-the-default-playback-behavior}

You can choose to use default ad behaviors.

To use default behaviors:

* If you implement your own `ContentFactory` class, return a new instance of `DefaultAdPolicySelector` in your implementation of `doRetrieveAdPolicySelector`.     

   ```
   public class CustomContentFactory extends ContentFactory { 
   
       //... 
       // your custom code for advertising classes 
       //... 
            
       /** 
        * @inheritDoc 
        */ 
       override protected function  
         doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new DefaultAdPolicySelector(item); 
       } 
   }
   ```

* If you do not have a custom implementation for the `ContentFactory` class, TVSDK uses `DefaultAdPolicySelector`.
