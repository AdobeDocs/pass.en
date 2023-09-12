---
description: You can insert ads into VOD content.
title: Replace time ranges with an ad
exl-id: f6675108-07a7-4d30-8a95-6029afe06ac5
---
# Replace time ranges with an ad {#replace-time-ranges-with-an-ad}

You can insert ads into VOD content.

The `TimeRanges` between the `begin` and `end` in `localTime` are removed from the timeline. These ranges are replaced by an `AdBreak` of `begin` to `begin+replaceDuration`. If the `replacement-duration` does not exist as a parameter, the server makes the determination on the returned `Adbreak`.

>[!TIP]
>
>You should always provide a `replacement-duration` for custom ranges. If no ads are intended to replace this custom range, provide a `replacement-duration` of 0.

1. To replace the ranges with Primetime ad decisioningads:

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 15000,
                           "replacement-duration": 15000
                       },
                       {
                                "begin": 69000,
                                "end": 99000,
                                "replacement-duration": 30000
                       },
                       {
                           "begin": 251000,
                           "end": 281000,
                           "replacement-duration": 30000
                       },
                       {
                           "begin": 514000,
                           "end": 544000,
                           "replacement-duration": 30000
                       }
                   ]
               },
               "ad": {
                   "targeting": [
                       {
                           "value": "MulAdsAvail12346",
                           "key": "osmfKeyMulAdsAvail12346"
                       }
                   ],
               "domain": "sandbox2.auditude.com",
               "mediaid": "psdk_000105",
               "zoneid": "121781"
               }     
           }
       },   
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```
