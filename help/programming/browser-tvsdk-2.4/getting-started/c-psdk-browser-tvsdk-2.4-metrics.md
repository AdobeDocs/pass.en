---
description: Browser TVSDK provides metrics to use for analyzing and debugging. You can get these metrics by using QoSProvider.
title: Metrics
exl-id: 1413ddf5-b458-4040-abf8-8d9dbd6b80e2
---
# Metrics{#metrics}

Browser TVSDK provides metrics to use for analyzing and debugging. You can get these metrics by using QoSProvider.

For example: 

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
