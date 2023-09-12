---
description: HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the available bandwidth.
title: Adaptive bit rates (ABR) for video quality
exl-id: 97862cf7-7315-4ca6-a2b4-f9b98047edd9
---
# Adaptive bit rates (ABR) for video quality {#adaptive-bit-rates-abr-for-video-quality}

HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the available bandwidth.

 TVSDK constantly monitors the bit rate to ensure that the content is played at the optimal bit rate for the current network connection.

You can set the adaptive bit-rate (ABR) switching policy and the initial, minimum, and maximum bit rates for a multiple-bit-rate (MBR) stream. TVSDK automatically switches to the bit rate that provides the best playback experience in the specified configuration. 

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Initial bit rate </td> 
   <td colname="col2"> <p>The desired playback bit rate (in bits per second) for the first segment. When playback starts, the closest profile, which is equal to or greater than the initial bit rate, is used for the first segment. </p> <p> If a minimum bit rate is defined, and the initial bit rate is lower than the minimum rate, TVSDK selects the profile with the lowest bit rate above the minimum bit rate. If the initial rate is above the maximum rate, TVSDK selects the highest rate below the maximum rate. </p> <p>If the initial bit rate is zero or undefined, the initial bit rate is determined by the ABR policy. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minimum bit rate </td> 
   <td colname="col2"> <p>The lowest allowed bit rate to which the ABR can switch. ABR switching ignores profiles with a bit rate that is lower than this bit rate. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximum bit rate </td> 
   <td colname="col2"> <p>The highest allowed bit rate to which the ABR can switch. ABR switching ignores profiles with a bit rate higher than this bit rate. </p> </td> 
  </tr> 
 </tbody> 
</table>

Keep the following information in mind:

* TVSDK does not dispatch events from bit-rate switching. 
* You can change your ABR settings at any time, and the player switches to use the profile that most closely matches the most recent settings.

For example, if a stream has the following profiles:

* 1: 300000 
* 2: 700000 
* 3: 1500000 
* 4: 2400000 
* 5: 4000000

If you specify a range of 300000 to 2000000, TVSDK considers only profiles 1, 2 and 3. This allows applications to adjust to various network conditions, such as switching from WiFi to 3G or to various devices such as a phone, a tablet, or a desktop computer.

## Configure adaptive bit rates {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

To configure TVSDK adaptive bit-rate parameters:

1. Configure an instance of `PTABRControlParameters` to set the initial, minimum, and maximum bit-rate settings.

   The default values are displayed in the following code snippet, but your application can set any integer value for each of these parameters. 

   >[!IMPORTANT]
   >
   >Specify the bit-rate settings in bits-per-second (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
    
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Update your `PTMediaPlayer` instance with the configured `PTABRControlParameters` instance. 

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Remember the following:

* The application must set the `abrControlParameters` property on `PTMediaPlayer` before configuring a `PTMediaPlayerItem` instance for the initial and minimum bitrate settings to take effect.

  After content playback starts, setting a new instance only affects the maximum bitrate setting. 

* To update the maximum bitrate setting during playback, create a new `PTABRControlParameters` instance and set it on the player instance. 
* You can update the maximum bitrate setting during playback only on iOS 8.0 and later. For earlier versions, the `maxBitrate` value that was set before content playback started is used.
