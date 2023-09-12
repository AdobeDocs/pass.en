---
description: If the application needs to handle events dispatched from the feature manager, it needs to register the manager in the PlayerFragment.java file.
title: Handling events
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
---
# Handling events {#handling-events}

If the application needs to handle events dispatched from the feature manager, it needs to register the manager in the PlayerFragment.java file.

For example:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
