---
description: To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.
title: Billing metrics
exl-id: 8b670ed0-77a5-410c-abd6-0188558fbc4a
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

Adobe pre-configures this arrangement, but if you want to change the arrangement, work with your Adobe Enablement representative.

To monitor the statistics that TVSDK sends to Adobe, obtain the URL from your Adobe Enablement representative, and use a network capture tool, for example, Charles, to see the data.

## Configure billing metrics {#configure-billing-metrics}

If you use the default configuration, there is nothing else you need to do to enable or configure billing. If you obtained different configuration parameters from your Adobe Enablement representative, use the PTBillingMetricsConfiguration class to set these parameters up before initializing the media player.

Most customers should use the default configuration.

>[!IMPORTANT]
>
>The configuration you set remains in effect for the life of the media player. Once you initialize the media player, you cannot change the configuration.

To configure billing metrics: 

1. Enter the following code sample.

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
                   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## Transmit billing metrics {#transmit-billing-metrics}

TVSDK sends billing metrics to Adobe in an XML format.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

If you use a network capture tool to monitor the statistics TVSDK transmits to Adobe, you should see units like the following:

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

The boolean properties `drmProtected`, `adsEnabled`, and `midrollEnabled` appear only if they are true.
