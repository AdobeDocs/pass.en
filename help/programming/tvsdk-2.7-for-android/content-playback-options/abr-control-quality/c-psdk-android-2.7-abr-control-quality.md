---
description: HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the current buffering level and the available bandwidth.
title: Adaptive bit rates (ABR) for video quality
exl-id: 76939ace-a7d1-40fc-a199-94b88d90535e
---
# Overview {#adaptive-bit-rates-abr-for-video-quality-overview}

HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the current buffering level and the available bandwidth.

 TVSDK constantly monitors the bit rate to ensure that the content is played at the optimal bit rate for the current network connection. You can set the adaptive bit rate (ABR) switching policy and the initial, minimum, and maximum bit rates for a multiple-bit-rate (MBR) stream. TVSDK automatically switches to the bit rate that provides the best playback experience in the specified configuration. 

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Initial bit rate </td> 
   <td colname="col2"> <p>The desired playback bit rate (in bits per second) for the first segment. </p> <p>When playback starts, the closest profile, which is equal to or greater than the initial bit rate, is used for the first segment. If a minimum bit rate is defined, and the initial bit rate is lower than the minimum rate, TVSDK selects the profile with the lowest bit rate above the minimum bit rate. If the initial rate is above the maximum rate, TVSDK selects the highest rate below the maximum rate. If the initial bit rate is zero or undefined, the initial bit rate is determined by the ABR policy. </p> <p><span class="codeph"> getABRInitialBitRate</span> returns an integer value that represents the byte-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minimum bit rate </td> 
   <td colname="col2"> <p>The lowest allowed bit rate to which the ABR can switch. </p> <p>ABR switching ignores profiles with a bit rate that is lower than this bit rate. <span class="codeph"> getABRMinBitRate</span> returns an integer value that represents the bits-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximum bit rate </td> 
   <td colname="col2"> <p>The highest allowed bit rate to which the ABR can switch. </p> <p>ABR switching ignores profiles with a bit rate higher than this bit rate. <span class="codeph"> getABRMaxBitRate</span> returns an integer value that represents the bits-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR switching policy </td> 
   <td colname="col2"> <p>Playback switches gradually to the highest-bit-rate profile when possible. You can set the policy for ABR switching, which determines how quickly TVSDK switches between profiles. The default is <span class="codeph"> ABR_MODERATE</span>. </p> <p>When TVSDK decides to switch to a higher bit rate, the player selects the ideal bit rate profile to switch to based on the current ABR policy: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Switches to the profile with the next higher bit rate when the bandwidth is 50% higher than the current bit rate. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Switches to the next higher bit rate profile when the bandwidth is 20% higher than the current bit rate. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Switches immediately to the highest bit-rate profile when the bandwidth is higher than the current bit rate. </li> 
     </ul> </p> <p>If the initial bit rate is zero, or is not specified but a policy is specified, playback starts with the lowest bit rate profile for a conservative policy, the profile closest to the median bit rate of available profiles for a moderate policy, and the highest bit rate profile for an aggressive policy. </p> <p>The policy works in the constraints of the minimum and maximum bit rates, if these rates are specified. </p> <p> <span class="codeph"> getABRPolicy</span> returns the current setting from the <span class="codeph"> ABRControlParameters</span> enum: <span class="codeph"> ABR_CONSERVATIVE</span>, <span class="codeph"> ABR_MODERATE</span>, or <span class="codeph"> ABR_AGGRESSIVE</span>. </p> <p>For more information, see ABRControlParameters API doc.</p> </td> 
  </tr> 
 </tbody> 
</table>

Keep the following information in mind:

* The TVSDK failover mechanism might override your settings, because TVSDK favors a continuous playback experience over strictly adhering to your control parameters. 
* When the bit rate changes, TVSDK dispatches `onProfileChanged` events in `PlaybackEventListener`. 

* You can change your ABR settings at any time, and the player switches to use the profile that most closely matches the most recent settings.

For example, if a stream has the following profiles:

* 1: 300000 
* 2: 700000 
* 3: 1500000 
* 4: 2400000 
* 5: 4000000

If you specify a range of 300000 to 2000000, TVSDK considers only profiles 1, 2 and 3. This allows applications to adjust to various network conditions, such as switching from wi-fi to 3G or to various devices such as a phone, a tablet, or a desktop computer.

To set ABR control parameters, set the parameters on the `ABRControlParameter` class.
