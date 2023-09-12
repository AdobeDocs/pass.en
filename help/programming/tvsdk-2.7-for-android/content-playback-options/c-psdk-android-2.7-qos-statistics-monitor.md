---
description: Quality of service (QoS) provides a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.
title: Quality of service statistics
exl-id: 084b5aa7-1eea-464b-a425-1da7b9fa1731
---
# Quality of service statistics {#quality-of-service-statistics}

Quality of service (QoS) provides a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.

 TVSDK also provides information about the following downloaded resources:

* Playlist/manifest files 
* File fragments 
* Tracking information for files

## Track at the fragment level using load information {#section_4439D91E8EDC45588EF1D7BE25697350}

You can read quality of service (QoS) information about downloaded resources, such as fragments and tracks, from the `LoadInformation` class.

1. Implement and register the `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` event listener. 
1. Call `event.getLoadInformation()` to read the relevant data from the `event` parameter that is passed to the callback. 

   >[!NOTE]
   >
   >For more about `LoadInformation`, see [2.7 for Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API docs.

## Read QOS playback, buffering, and device statistics {#section_D21722600F324E67A9F06234D338B243}

You can read playback, buffering, and device statistics from the `QOSProvider` class.

The `QOSProvider` class provides various statistics, including information about buffering, bit rates, frame rates, time data, and so on. It also provides information about the device, such as the manufacturer, model, operating system, SDK version, manufacturer's device ID, and screen size/density.

1. Instantiate a media player. 
1. Create a `QOSProvider` object and attach it to the media player.

   The `QOSProvider` constructor takes a player context so that it can retrieve device-specific information. 

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Optional) Read the playback statistics.

   One solution to read playback statistics is to have a timer, that periodically fetches the new QoS values from the `QOSProvider`.

   For example: 

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   
   ```

1. (Optional) Read the device-specific information. 

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
    
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
    
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   
   ```
