---
description: Browser TVSDK provides a DRM interface you can use to play content protected by different DRM solutions, including FairPlay, PlayReady, and Widevine.
title: DRM interface overview
exl-id: aa13f042-4472-4fc3-b7ba-61746b8e024a
---
# DRM interface overview{#drm-interface-overview}

Browser TVSDK provides a DRM interface you can use to play content protected by different DRM solutions, including FairPlay, PlayReady, and Widevine.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM support is available for MPEG-Dash streams protected with Microsoft PlayReady (on Internet Explorer on Windows 8.1 and Edge), and Widevine (on Google Chrome) DRM systems. DRM support is available for HLS streams on Safari that are protected with FairPlay.

The key interface of the DRM workflow is the `DRMManager`. A reference to the `DRMManager` instance can be obtained through the MediaPlayer instance:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();` 
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Here is a high-level workflow for playback of DRM-protected content:

1. To attach the DRM-system specific data that will be used by Browser TVSDK in the license acquisition process for a protected stream, make the following call before invoking `mediaPlayer.replaceCurrentResource`: 

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. If the same content is expected to work with different DRM systems in different browsers, protection data can be specified for multiple DRM systems. 

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
    
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. When protection data is not set, necessary information such as the license URL, is retrieved from the PSSH box for DRM systems where applicable. 

   >[!TIP]
   >
   >Specifying protection data overrides the license URL that is specified in the PSSH box.

1. By default, the session type for the DRM license is temporary, which means that the license is not stored after the session is closed.

   You can specify a session type using an API in `DRMManager`.  For backward compatibility, session types include `temporary`, `persistent-license`, `persistent-usage-record`, and `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   
   ```

1. When the `sessionType` used is `persistent-license` or `persistent`, the DRM license can be returned by invoking `DRMManager.returnLicense`. 

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
    
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
    
   drmManager = mediaPlayer.drmManager; 
    
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```
