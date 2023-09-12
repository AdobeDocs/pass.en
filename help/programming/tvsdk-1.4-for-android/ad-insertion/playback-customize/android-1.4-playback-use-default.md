---
description: You can choose to use default ad behaviors.
title: Use the default playback behavior
exl-id: c277db2a-546e-4097-96ce-83914b726576
---
# Use the default playback behavior {#use-the-default-playback-behavior}

You can choose to use default ad behaviors.

   To use default behaviors:

    * If you implement your own `AdvertisingFactory` class, return null for `createAdPolicySelector` . 
    
    * If you do not have a custom implementation for the `AdvertisingFactory` class, TVSDK uses  a default ad policy selector .
