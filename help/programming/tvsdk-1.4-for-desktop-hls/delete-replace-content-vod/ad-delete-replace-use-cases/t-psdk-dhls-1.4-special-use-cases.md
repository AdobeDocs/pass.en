---
title: Special Use Cases
description: Special Use Cases
copied-description: yes
exl-id: 33aad8cc-5939-4890-bc89-32d6bbf1fa4c
---
# Special Use Cases{#special-use-cases}

TVSDK favors custom range settings over standard ad settings. For example, if MARK ranges are defined, the ad's insertion settings are ignored. If REPLACE ranges are defined, TVSDK automatically uses the `CustomRanges` signaling mode. 

1. `ReplaceRange` without replacement duration

   If the replacement duration is missing, the actual replacement duration is determined by the server. The number of ads placed in this `AdBreak` is also determined by the server. 

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   
   ```

1. MARK and DELETE ranges with replacement duration

   The extra replacement duration is ignored.
