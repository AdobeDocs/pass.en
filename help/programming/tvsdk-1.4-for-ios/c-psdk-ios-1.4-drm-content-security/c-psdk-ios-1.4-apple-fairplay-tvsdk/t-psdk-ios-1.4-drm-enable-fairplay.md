---
description: You can implement Apple FairPlay Streaming, which is Apple's DRM solution, in your TVSDK applications.
title: Enable Apple FairPlay in TVSDK applications
---

# Enable Apple FairPlay in TVSDK applications{#enable-apple-fairplay-in-tvsdk-applications}

You can implement Apple FairPlay Streaming, which is Apple's DRM solution, in your TVSDK applications.

1. Create your FairPlay Customer Resource Loader by implementing `PTAVAssetResourceLoaderDelegate`.

   For more information, see [Apple FairPlay in TVSDK applications](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md). 

   >[!NOTE]
   >
   >Ensure that you follow the instructions in the *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), which is included in [FairPlay Server SDK for Developing a FPS-Aware App](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   The `resourceLoader:shouldWaitForLoadingOfRequestedResource` method is equivalent to what is in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >In the ExpressPlay license server scenario, to play back content, change the URL scheme in your ExpressPlay FairPlay server license request URL from `skd://` to `https://` (or `https://`).

1. Register the *FairPlay* Customer Resource Loader with `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

If you wrote your own FairPlay license server, or you are using a third-party FairPlay license server, consult your license server vendor to determine your license server URL, formatting, and any other requirements. 
