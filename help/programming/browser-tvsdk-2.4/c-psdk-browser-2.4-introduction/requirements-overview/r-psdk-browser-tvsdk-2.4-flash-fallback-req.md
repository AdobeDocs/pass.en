---
description: To use Flash Player, ensure that your environment meets the necessary requirements.
title: Flash Player requirements
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
---
# Flash Player requirements{#flash-player-requirements}

To use Flash Player, ensure that your environment meets the necessary requirements.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Here are the requirements for the Flash Player:

* To play back with `Primetime.js`, install at least Flash Player version 23. 
* To be prompted for updates to Flash Player version 23 or later, install at least Flash Player version 11.0.0.

## Packaging requirements {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

Playback with Flash Player requires the following SWF files:

* The main application SWF file that handles Browser TVSDK APIs. 
* The `playerProductInstall.swf` SWF file that handles Flash Player installation and updates.

In addition, video playback in Flash requires an authorization token file that might be a SWF or a `.DAT` file. The path to the SWF files, the authorization token file, and the token file name and type can be specified by using the AdobePSDK APIs.

For example: 

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```
