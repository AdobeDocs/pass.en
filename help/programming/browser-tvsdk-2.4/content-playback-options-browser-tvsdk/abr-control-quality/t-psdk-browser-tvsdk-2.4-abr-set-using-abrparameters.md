---
description: You can set ABR control values only with ABRControlParameters, but you can construct a new one at any time.
title: Configure adaptive bit rates using ABRControlParameters
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
---
# Configure adaptive bit rates using ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

You can set ABR control values only with ABRControlParameters, but you can construct a new one at any time.

 The following conditions apply to `ABRControlParameters`:

* You must provide values for all parameters at construction time. 
* You cannot change individual values after construction time. 
* If the parameters that you specify are outside of the allowed range, an `ArgumentError` is thrown.

1. Determine the ABR policy:

    * `ABRControlParameters.CONSERVATIVE_POLICY` 
    * `ABRControlParameters.MODERATE_POLICY` 
    * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Set the ABR parameter values in the `ABRControlParameters` constructor and assign them to the Media Player.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
