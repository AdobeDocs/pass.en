---
description: To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.
title: Billing metrics
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
---
# Overview {#billing-metrics-overview}

To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.

Every time the player generates a stream start event, Browser TVSDK starts to send HTTP messages periodically to Adobe's billing system. The period, known as billable duration, can be different for standard VOD, pro VOD (mid-roll ads enabled), and live content. The default duration for each content type is 30 minutes, but your contract with Adobe determines the actual values.

The messages contain the following information:

* Content type (live, linear, or VOD) 
* Content URL 
* Whether ads are enabled 
* Whether mid-roll ads are enabled (VOD only) 
* Whether the stream is protected by DRM 
* The Browser TVSDK version and platform

Adobe pre-configures this arrangement, but if you want to change the arrangement, work with your Adobe Enablement representative.

To monitor the statistics that Browser TVSDK sends to Adobe, obtain the URL from your Adobe Enablement representative, and use a network capture tool, for example, Charles, to see the data.
