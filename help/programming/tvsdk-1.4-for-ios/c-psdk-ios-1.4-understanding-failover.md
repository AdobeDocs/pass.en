---
description: Failover handling occurs when a variant playlist has multiple renditions for the same bit rate, and one of the renditions stops working. The TVSDK switches between renditions.
title: Failover
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
---
# Failover{#failover}

Failover handling occurs when a variant playlist has multiple renditions for the same bit rate, and one of the renditions stops working. The TVSDK switches between renditions.

The following example shows a variant playlist with failover URLs of the same bit rate: 

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

When TVSDK loads the variant playlist, it creates a queue that holds the URLs for all the renditions of the content for the same bit rate. When a request for a URL fails, TVSDK uses the next URL of the same bit rate from the failover queue. At any specific failure time, TVSDK cycles once through all available URLs until it finds one that works correctly or until it has attempted all the available URLs. If TVSDK has tried to all of the available URLs and none of the URLs work, TVSDK stops trying to play the content.

Failover occurs only at the M3U8 level, which means:

* For VOD, failover can occur only when it begins to attempt to play and not after it has started playing. 
* For live streaming, failover can happen in the middle of the stream.

>[!TIP]
>
>TVSDK, rather than the Apple AV Foundation player, provides failover handling.
