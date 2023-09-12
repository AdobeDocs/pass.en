---
description: To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.
title: Billing metrics
exl-id: 6e839f59-dd1e-4037-96a9-8b35b361988f
---
# Billing metrics {#billing-metrics}

To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.

Every time the player generates a stream start event, TVSDK starts to send HTTP messages periodically to Adobe's billing system. The period, known as billable duration, can be different for standard VOD, pro VOD (mid-roll ads enabled), and live content. The default duration for each content type is 30 minutes, but your contract with Adobe determines the actual values.

The messages contain the following information:

* Content type (live, linear, or VOD) 
* Content URL 
* Whether ads are enabled 
* Whether mid-roll ads are enabled (VOD only) 
* Whether the stream is protected by DRM 
* The TVSDK version and platform

Adobe preconfigures this arrangement, but you can work with your Adobe Enablement representative to change the arrangement, work with your Adobe Enablement representative.

To monitor the statistics that TVSDK sends to Adobe, obtain the URL from your Adobe Enablement representative, and use a network capture tool, like Charles, to see the data.
