---
description: HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the available bandwidth.
title: Adaptive bit rates (ABR) for video quality
exl-id: 2fd24360-4159-4330-a479-02310c6aa525
---
# Adaptive bit rates (ABR) for video quality{#adaptive-bit-rates-abr-for-video-quality}

HLS and DASH streams provide different bit rate encodings (profiles) for the same short burst of video. TVSDK can select the quality level for each burst based on the available bandwidth.

 TVSDK constantly monitors the bit rate to ensure that the content is played at the optimal bit rate for the current network connection.

You can set the adaptive bit-rate (ABR) switching policy and the initial, minimum, and maximum bit rates for a multiple-bit-rate (MBR) stream. TVSDK automatically switches to the bit rate that provides the best playback experience in the specified configuration. 

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Initial bit rate </td> 
   <td colname="col2"> <p>The desired playback bit rate (in bits per second) for the first segment. When playback starts, the closest profile, which is equal to or greater than the initial bit rate, is used for the first segment. </p> <p> If a minimum bit rate is defined, and the initial bit rate is lower than the minimum rate, TVSDK selects the profile with the lowest bit rate above the minimum bit rate. If the initial rate is above the maximum rate, TVSDK selects the highest rate below the maximum rate. </p> <p>If the initial bit rate is zero or undefined, the initial bit rate is determined by the ABR policy. </p> <p> <span class="apiname"> ABRInitialBitRate </span> returns an integer value that represents the byte-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Minimum bit rate </td> 
   <td colname="col2"> <p>The lowest allowed bit rate to which the ABR can switch. ABR switching ignores profiles with a bit rate that is lower than this bit rate. </p> <p> <span class="apiname"> ABRMinBitRate </span> returns an integer value that represents the bits-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Maximum bit rate </td> 
   <td colname="col2"> <p>The highest allowed bit rate to which the ABR can switch. ABR switching ignores profiles with a bit rate higher than this bit rate. </p> <p> <span class="apiname"> ABRMaxBitRate </span> returns an integer value that represents the bits-per-second profile. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> ABR switching policy </td> 
   <td colname="col2"> Playback switches gradually to the highest-bit-rate profile when possible. You can set the policy for ABR switching, which determines how quickly TVSDK switches between profiles. The default is <span class="codeph"> MODERATE_POLICY </span>. <p>When TVSDK decides to switch to a higher bit rate, the player selects the ideal bit rate profile to switch to based on the current ABR policy: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: Switches to the profile with the next higher bit rate when the bandwidth is 50% higher than the current bit rate. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: Switches to the next higher bit rate profile when the bandwidth is 20% higher than the current bit rate. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY </span>: Switches immediately to the highest bit-rate profile when the bandwidth is higher than the current bit rate. </li> 
     </ul> </p> <p>If the initial bit rate is zero or is not specified, but a policy is specified, playback starts with the lowest bit rate profile for conservative, the profile closest to the median bit rate of available profiles for moderate, and the highest bit rate profile for aggressive. </p> <p>The policy works in the constraints of the minimum and maximum bit rates, if these rates are specified. </p> <p> <span class="codeph"> ABRPolicy </span> returns the current setting from the <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY, or AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Keep the following information in mind:

* The TVSDK failover mechanism might override your settings, because TVSDK favors a continuous playback experience over strictly adhering to your control parameters. 
* When the bit rate changes, TVSDK dispatches `ProfileEvent.PROFILE_CHANGED`. 
* You can change your ABR settings at any time, and the player switches to use the profile that most closely matches the most recent settings.

For example, if a stream has the following profiles:

* 1: 300000 
* 2: 700000 
* 3: 1500000 
* 4: 2400000 
* 5: 4000000

If you specify a range of 300000 to 2000000, TVSDK considers only profiles 1, 2 and 3. This allows applications to adjust to various network conditions, such as switching from wi-fi to 3G or to various devices such as a phone, a tablet, or a desktop computer.

To set ABR control parameters, do one of the following:

* Use the `ABRControlParameterBuilder` helper class to set any subset of the parameters (operates on `ABRControlParameter` behind the scenes) 

* Set the parameters on the `ABRControlParameter` class.

## Configure adaptive bit rates using ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Using the `ABRControlParametersBuilder` helper class is the simplest, most efficient way to set ABR parameters.

* The `ABRControlParametersBuilder` constructor sets all of the ABR parameters to default values on the underlying `ABRControlParameters` object. 

* You can reset individual ABR parameters during run time, as long as you maintain a reference to the same `ABRControlParametersBuilder` instance.

This class also includes the `toABRControlParameters()` helper method. Use this method to get an instance of `ABRControlParameters` and set it on the `mediaPlayer.ABRControlParameters` property. This causes your settings to go into effect in the player.

1. Instantiate the `ABRControlParametersBuilder` helper class, and set the parameters on the Media Player. 

   >[!NOTE]
   >
   >For example, the following sample initializes all parameters to the defaults, then sets only the policy to conservative, and restricts the maximum bit rate to 1000000:
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >  new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >  abrBuilder.toABRControlParameters();
   >```
   >

1. Modify individual ABR parameters at run time.

   To modify individual parameters while leaving the rest of the parameters as they were:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   To retain your previous settings, you must maintain a reference to the same `ABRControlParametersBuilder` instance you created in Step 1.

## Configure adaptive bit rates using ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

You can set ABR control values only with `ABRControlParameters`, but you can construct a new one at any time.

This ability to set ABR parameters was supported before the existence of the `ABRControlParametersBuilder` class, but this ability is still effective for setting ABR parameters at construction time. However, to change individual parameters after construction, you should use the `ABRControlParametersBuilder` class.

The following conditions apply to `ABRControlParameters`:

* You must provide values for all parameters at construction time. 
* You cannot change individual values after construction time. 
* If the parameters that you specify are outside of the allowed range, an `ArgumentError` is thrown.

1. Decide on initial, minimum, and maximum bit rates. 
1. Determine the ABR policy:

    * `CONSERVATIVE_POLICY` 
    * `MODERATE_POLICY` 
    * `AGGRESSIVE_POLICY`

1. Set the ABR parameter values in the `ABRControlParameters` constructor and assign them to the Media Player. 

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
