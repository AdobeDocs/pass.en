---
description: You can set ABR control values only with ABRControlParameters, but you can construct a new one at any time.
title: Configure adaptive bit rates using ABRControlParameters
exl-id: fc7887bd-37e8-48e7-8afb-3946fb3f1e77
---
# Configure adaptive bit rates using ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

You can set ABR control values only with ABRControlParameters, but you can construct a new one at any time.

 The following conditions apply to `ABRControlParameters`:

* At construction time, you must provide values for all parameters. 
* After the construction, you cannot change individual values. 
* If the parameters that you specify are outside of the allowed range, an `ArgumentError` is thrown.

1. Determine your initial, minimum, and maximum bit rates.
1. Determine the ABR policy:

    * `ABR_CONSERVATIVE` 
    * `ABR_MODERATE` 
    * `ABR_AGGRESSIVE`

1. Set the ABR parameter values in the `ABRControlParameters` constructor and assign the values to the Media Player.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
