---
description: If you use the default configuration, there is nothing else you need to do to enable or configure billing. If you obtained different configuration parameters from your Adobe Enablement representative, use the BillingMetricsConfiguration class to set these parameters up before initializing the media player.
title: Configure billing metrics
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
---
# Configure billing metrics{#configure-billing-metrics}

If you use the default configuration, there is nothing else you need to do to enable or configure billing. If you obtained different configuration parameters from your Adobe Enablement representative, use the BillingMetricsConfiguration class to set these parameters up before initializing the media player.

Most customers should use the default configuration.

>[!IMPORTANT]
>
>The configuration you set remains in effect for the life of the media player. Once you initialize the media player, you cannot change the configuration.

To configure billing metrics: 

* Enter the following code sample.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   where `_player` is an instance of `AdobePSDK.MediaPlayer` and `_resource` is an instance of `AdobePSDK.MediaResource`.
