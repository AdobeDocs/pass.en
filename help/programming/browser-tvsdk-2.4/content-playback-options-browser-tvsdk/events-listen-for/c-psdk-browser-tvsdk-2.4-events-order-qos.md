---
description: Browser TVSDK dispatches quality of service (QoS) events to notify your application about events that could influence the computation of QoS statistics, such as buffering and seeking events.
title: QoS events
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
---
# QoS events{#qos-events}

Browser TVSDK dispatches quality of service (QoS) events to notify your application about events that could influence the computation of QoS statistics, such as buffering and seeking events.

To be notified about all QoS-related events, create an instance of `AdobePSDK.QOSProvider` and attach the MediaPlayer instance to this `QOSProvider` instance: 

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure a timer in your application to periodically check the `playbackInformation` property of the `qosProvider` instance. The `playbackInformation` property provides a snapshot of the current playback statistics. For example: 

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 

```
