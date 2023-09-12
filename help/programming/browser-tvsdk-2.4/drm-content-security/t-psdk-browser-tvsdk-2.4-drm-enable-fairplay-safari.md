---
description: You can enable FairPlay for Safari when working with Primetime DRM Cloud, powered by ExpressPlay.
title: Enable FairPlay for Safari HLS
exl-id: 761c7cb8-3068-44c9-8ceb-6411c509c0a7
---
# Enable FairPlay for Safari HLS {#enable-fairplay-for-safari-hls}

You can enable FairPlay for Safari when working with Primetime DRM Cloud, powered by ExpressPlay.

Ensure you have the following:

* A functioning sample app that can play HLS video.

  The sample app must be able to play FairPlay-protected content with the licensing handled through Primetime DRM powered by ExpressPlay. 
* Sample HLS content (an M3U8 manifest) packaged with FairPlay protection.

To make full use of the information here, learn about Multi-DRM Workflows starting with the sub-section [Reference Server: Sample ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) in the Multi-DRM Workflows guide. First read that documentation on how to set up your entitlement and key server, and the information below will be much more useful.
You need the following items:

* Your *production* Customer Authenticator from ExpressPlay 
* The same Content Key and `iv` with which your content was packaged. 
* The location of your FairPlay public key certificate.

To modify your FairPlay / Safari app:

1. Set the location of your FairPlay public key cert that was used in the FairPlay license server request.

   For example: 

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Perform a manual FairPlay license *token* request to ExpressPlay to obtain a license token URL.

       You can complete this step in one of the following ways:

    * Use your own ExpressPlay Production Customer Authenticator. 
    * Use the same Content Key and `iv` in this request that was used to package the content you want to play.

       Run the following command from the shell and substitute your ExpressPlay customer authenticator to obtain the license token URL for the sample content:

       ```    
       curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
            customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
            errorFormat=json& 
            contentKey=<your content key>& 
            iv=<your iv here>"
       ```    
    
       The response with the license token URL will look something like this:

       ```    
       https://fp.service.expressplay.com:80/hms/fp/rights/? 
            ExpressPlayToken=<base64-encoded ExpressPlay token>
       ```

1. Set a variable with the license token URL from ExpressPlay.

   For example: 

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Before your app can play protected content, change the URL scheme for the content from `skd://` to `https://`.

   You need to add this URL scheme change in your app, before the call to the license server that allows playback.

   The protocols need to be changed because the Content ID, which provides access to the Content Key in the Key Management System, is packaged in the M3U8 manifest with the `skd://` protocol. When the player is ready to get the license to play the protected content, it needs to first switch protocols to communicate with the ExpressPlay license server. In the example below, the `myServerProcessSPCPath` is modified to contain the correct URL scheme for the license server request:

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```
