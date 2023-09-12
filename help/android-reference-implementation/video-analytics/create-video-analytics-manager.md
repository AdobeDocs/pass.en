---
description: Create the Video Analytics Manager
title: Create the Video Analytics Manager
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
---
# Create the Video Analytics Manager {#create-the-video-analytics-manager}

A new manager class ( `VAManager`) has been added to the Android Reference Implementation. `VAManager` simply creates and destroys an instance of the `VideoHeartbeat` class. The reference implementation creates a `VAManager` instance when a new `MediaPlayer` is created, and destroys that instance when the `MediaPlayer` is destroyed. This is implemented in `PlayerFragment.java`. 

## To create a new Video Analytics Manager

   ```java
   VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
   vaManager.createVAProvider(getActivity().getApplicationContext()); 
   ```

   The config variable is a concrete implementation of `IVAConfig` and contains the runtime `VideoHeartbeat` configurations.

   >[!NOTE]
   >
   >If the Android application is not configured with an Adobe Analytics account, then video tracking data will not be generated, even if an instance of `VAManager` is created and enabled.
