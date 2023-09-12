---
description: You can track video usage in the Primetime Android Reference Implementation by configuring it to work with your Adobe Analytics account.
title: Configure Video Analytics
exl-id: 42498e2a-9ff2-442c-8cf9-bd7901f618f4
---
# Configure Video Analytics {#configure-video-analytics}

You can track video usage in the Primetime Android Reference Implementation by configuring it to work with your Adobe Analytics account. The Android Reference Implementation is designed to send video usage and heartbeat data to Adobe Analytics. To enable this feature, you must first contact your Adobe Primetime representative and create an Adobe Analytics account.

There are two places within the Reference Implementation that you must configure to enable the Adobe Analytics integration. The run-time Video Analytics configurations take affect once a new video is selected for playback (i.e. once a new PlayerActiviy is created). 

1. Configure load-time options in the `ADBMobileConfig.json` assets file.

   This file is provided by your Adobe representative. It is not included in the Primetime SDK bundle by default. For more information on the settings in this config file, see the Android Programmer's Guide here: Initialize and configure video analytics.
1. Configure run-time options in the Reference Implementation settings menu

   ![](assets/img_psdk_ref_impl_va-settings-menu.png) 

   |  Run-time Options | Description |
   |---|---|
   |  Video Analytics tracking server | URL of the video analytics back-end collection end-point. This is where all video heartbeat tracking calls are sent. |
   |  Job ID | The processing job identifier. This indicates to the back-end endpoint which kind of processing to apply for the video-tracking calls. |
   |  Channel | The name of the channel where the user is watching the content. For a mobile application, this is typically the name of the application. |
   |  Publisher | The name of the content publisher |
   |  Debug Logging | Activates extensive logging. Disabled by default, this can impact performance when enabled, so you disable this for a production environment. |
   |  Quiet Mode | When this is enabled, no network calls are made, so this would be useful for local debugging, but must be disabled for a production environment. |
