---
description: Quality of service (QoS) offers a detailed view into how the video engine is performing. Browser TVSDK provides detailed statistics about playback, buffering, and devices.
title: Quality of service statistics
exl-id: b7486ed5-e59f-428c-942c-a2fee7a869c9
---
# Quality of service statistics{#quality-of-service-statistics}

Quality of service (QoS) offers a detailed view into how the video engine is performing. Browser TVSDK provides detailed statistics about playback, buffering, and devices.

## Read QOS playback, buffering, and device statistics {#read-qos-playback-buffering-and-device-statistics}

You can read playback, buffering, and device statistics from the QOSProvider class.

The `QOSProvider` class provides various statistics, including information about buffering, bit rates, frame rates, time data, and so on. 

1. Instantiate a media player.
1. Create a `QOSProvider` object and attach it to the media player.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Optional) Read the playback statistics.

   One solution to read playback statistics is to have a timer, that periodically fetches the new QoS values from the `QOSProvider`. For example:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
    
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
    
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
    
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
    
   qosTimer.start(); 
   
   ```

1. (Optional) Read the device-specific information.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
