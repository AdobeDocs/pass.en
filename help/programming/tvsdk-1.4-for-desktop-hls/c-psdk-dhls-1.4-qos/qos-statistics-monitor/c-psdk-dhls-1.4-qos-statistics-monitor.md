---
description: Quality of service (QoS) offers a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.
title: Quality of service statistics
exl-id: ab664d75-a24f-41d6-91d7-a26ad7baab9a
---
# Quality of service statistics {#quality-of-service-statistics}

Quality of service (QoS) offers a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.

 TVSDK also provides information about the following downloaded resources:

* Playlist/manifest files 
* File fragments 
* Tracking information for files

## Track at the fragment level using load information {#track-at-the-fragment-level-using-load-information}

You can read quality of service (QoS) information about downloaded resources, such as fragments and tracks, from the LoadInformation class.

1. Implement the `onLoadInformationAvailable` callback event listener.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Register the event listener, which TVSDK calls every time a fragment has downloaded.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Read the data of interest from the `LoadInformation` that is passed to the callback.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Property </th> 
      <th colname="col1" class="entry"> Type </th> 
      <th colname="col2" class="entry"> Description </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>Number </p> </td> 
      <td colname="col2"> <p>The duration of the download in milliseconds. </p> <p>TVSDK does not differentiate between the time it took the client to connect to the server and the time it took to download the full fragment. For example, if a 10 MB segment takes 8 seconds to download, TVSDK provides that information, but does not tell you that it took 4 seconds until the first byte and another 4 seconds to download the entire fragment. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Number </p> </td> 
      <td colname="col2"> The media duration of the downloaded fragments in milliseconds. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size </span> </td> 
      <td colname="col1"> <p>Number </p> </td> 
      <td colname="col2"> The size of the downloaded resource in bytes. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> The index of the corresponding track, if known; otherwise, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> The name of the corresponding track, if known; otherwise, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> The type of the corresponding track, if known; otherwise, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> What TVSDK downloaded. One of the following: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - A playlist/manifest </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENT - A fragment </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - A fragment associated with a specific track </li> 
      </ul> Sometimes it might not be possible to detect the type of the resource. If this occurs, FILE is returned. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> The URL that points to the downloaded resource. </td> 
   </tr> 
   </tbody> 
   </table> 

## Read QOS playback, buffering, and device statistics {#read-qos-playback-buffering-and-device-statistics}

You can read playback, buffering, and device statistics from the QOSProvider class.

The `QOSProvider` class provides various statistics, including information about buffering, bit rates, frame rates, time data, and so on.

It also provides information about the device, such as the manufacturer, model, operating system, SDK version, and screen size/density.

1. Instantiate a media player.
1. Create a `QOSProvider` object and attach it to the media player.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Optional) Read the playback statistics.

   One solution to read playback statistics is to have a timer, that periodically fetches the new QoS values from the `QOSProvider`. For example: 

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (Optional) Read the device-specific information.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```
