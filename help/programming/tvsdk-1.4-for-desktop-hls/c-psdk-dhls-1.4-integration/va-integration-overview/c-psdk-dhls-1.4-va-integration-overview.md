---
description: You can track video use by integrating TVSDK with Adobe Analytics.
title: Video analytics
exl-id: 02303511-2713-4974-ada7-6f50fc500325
---
# Video analytics{#video-analytics}

You can track video use by integrating TVSDK with Adobe Analytics.

Video tracking in TVSDK uses the **Adobe Analytics Video Essentials** service, which provides video engagement metrics, such as video views, video completes, ad impressions, time spent on video, and so on. For more information about this service, contact your Adobe representative.

The following procedure summarizes the steps to activate video tracking in your player:

1. Initialize and/or configure the following video tracking components:

    * **AppMeasurement library** - Contains the low-level data collection core logic. This is where the video heartbeat data is accumulated and sent over the network. 
    * **Video heartbeat library** - Contains the video-heartbeat data collection core logic. The video heartbeat library accesses a subset of the `AppMeasurement` library APIs.     
    
      >[!TIP]
      >
      >Your app does not interact directly with the video heartbeat code. Instead, the app uses TVSDK APIs to configure your player's video tracking capabilities.

    * **VisitorID Library** - Uniquely identifies visitors to the web page that hosts the video player.

   >[!IMPORTANT]
   >
   >The TVSDK built-in video tracking capability depends on a properly configured `AppMeasurement` instance. The tracking elements assume that the `AppMeasurement` library is already instantiated and configured before configuring and activating video tracking. TVSDK video tracking capabilities depend on the existence of a fully functional and properly configured instance of the `AppMeasurement` library.

1. Set up video analytics reporting on the server side by using Adobe Analytics Admin Tools.
