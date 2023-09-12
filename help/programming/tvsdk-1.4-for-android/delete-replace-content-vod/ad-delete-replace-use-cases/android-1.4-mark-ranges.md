---
description: You can designate time intervals in VOD content as ad breaks.
title: Mark ranges
exl-id: cd661327-20b2-4a49-8002-6ecee86c2a2c
---
# Mark ranges{#mark-ranges}

You can designate time intervals in VOD content as ad breaks.

In this case, `TimeRanges` between the `begin` and `end` in `localTime` will be marked as an `AdBreak` in the timeline. Other Ad settings are ignored.

>[!NOTE]
>
>If you only want to mark certain ranges in the content as ads (with no dynamic ad insertion), create a `CustomRangeMetadata` instance, and specify the type as a MARK operation with the defined custom ranges.

1. Mark ranges.

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
                       "begin": 0,
                       "end": 15000
                    },
                    {
                        "begin": 69000,
                        "end": 99000
                    },
                    {
                        "begin": 251000,
                        "end": 281000
                    },
                    {
                        "begin": 514000,
                        "end": 544000
                    } ]
               }
           }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   
   ```
