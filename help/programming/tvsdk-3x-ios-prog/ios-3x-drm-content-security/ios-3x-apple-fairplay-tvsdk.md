---
description: To implement FairPlay Streaming in your TVSDK app, you need to write a Resource Loader, which sends a license acquisition request to your FairPlay Streaming server.
title: Apple FairPlay in TVSDK applications
exl-id: 44bc076d-77bd-4fbc-9813-4146546ec264
---
# Apple FairPlay in TVSDK applications {#apple-fairplay-in-tvsdk-applications}

To implement FairPlay Streaming in your TVSDK app, you need to write a Resource Loader, which sends a license acquisition request to your FairPlay Streaming server.

The Resource Loader code is responsible for the following tasks:

1. Determine where to send the license acquisition request. 
1. Format the request. 
1. Provide the necessary information to the server, so that the server can decide whether the request should be permitted.

For example, if you are using Adobe's Primetime Cloud DRM powered by ExpressPlay, your Resource Loader sends the request to: 

```
https://fp-gen.service.expressplay.com
```

The Resource Loader formats the request and attaches an ExpressPlay token that authorizes playback to the URL. When acquiring the ExpressPlay token, there are several options to consider. These options are determined by how you packaged your content.

When you package your content, the packager inserts `skd:` URLs in your M3U8 manifest. After the `skd:` entry, you can put any data in the manifest. You can use this data in your application code to complete the tasks that are listed above. For example, you can use `skd:{content_id}` so that your app can determine the ID of the content that is being played and request a token for that specific piece of content. You can also, for example, use `skd:{entitlement_server_url}?cid={content_id}`, so that your app does not need to have the entitlement server URL hardcoded.

You might not need any information in your `skd:` URL if, when playback starts, you already know the Content ID through other channels. The second example is an ideal solution to test your set up, but you can also use it in a production environment.

>[!TIP]
>
>You determine the format of `skd:`.

Your content is obtained by using the `skd:` protocol, but your license request uses `https:`. The most common options to deal with these protocols are:

* **Initial testing of end-to-end playback** When packaging your content, select a `skd:` URL. When testing your app, manually acquire a license from ExpressPlay and hardcode the license (an `https:` URL) and content URL in your loader.

  For example: 

  ```
  NSString* const PLAYLIST_URL =  
    @"https://{your_content_URL}/{your_manifest}.m3u8"; 
  NSString* const EXPRESSPLAY_TOKEN =  
    @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
      ExpressPlayToken={copy_your_token_to_here}";
  ```

* **Most other cases** When packaging your content, select a `skd:` URL that uniquely represents the ID of the content. In your loader, parse the `skd:` URL, send it to your server to acquire a token, and use the resulting token as the URL.

  For example: 

  ```
  - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
        shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
      NSURL *url = [[loadingRequest request] URL]; 
      if (![[url scheme] isEqual:@"skd"]) 
          return NO; 
       
      NSString *strUrl = [url absoluteString]; 
      NSLog(@"url is: %@", strUrl); 
       
      strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
       
      NSData *assetId; 
       
      NSData *requestBytes; 
      NSError* error = nil; 
      BOOL handled = NO; 
       
      NSData  *responseData = nil; 
       
      assetId = getMyAssetIdentifierFromURL(url); 
       
      /* Usecase 1: "On Premise Fairplay Server" 
       * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
       * Server Url is either hardcoded in the App or derived from strUrl. 
       */ 
  #if 0  
      // Insert your use case 1 codes here: 
      // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
  #endif // 
       
      /* Usecase 2: The strUrl is the entitlement server. 
       * Send assetId to the entitlement server; if the user is allowed to playback  
       * the content, the entitlement server will send back an ExpressPlay Token Url. 
       */ 
       
  #if 0 
      // The hardcoded SEES server: 
      strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
   
      // You can use the following code to simulate a device binding entitlement  
      // request:  
      // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
      // bEnforceDeviceID set to false. When you play the content, the device_id  
      // will be registered on the ExpressPlay Server.  Now change code to set  
      // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
      // sent back by the SEES server will be device bound. 
       
      // The strUrl returned below is the ExpressPlay Token URL. 
      strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
  #endif 
   
      /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
       */ 
       
      // Read in the certificate 
      NSLog(@"Get Application Certificate"); 
      NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                           ofType:nil]; 
       
      NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
       
      // To create the request blob for the server: 
      requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                        contentIdentifier:assetId  
                                                                  options:nil  
                                                                    error:&error]; 
      if (requestBytes == nil) { 
          NSLog(@"Error creating server request: %@", error); 
          return false; 
      } 
      // Per the specification, send requestBytes along with the assetId to the Key 
      // Server and obtain the response. 
      NSError *err; 
       
      responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
       
      if (responseData != nil) { 
          NSLog(@"Get response data: "); 
          [loadingRequest finishLoadingWithResponse:nil  
                                               data:(NSData *)responseData 
                                           redirect:nil]; 
      } 
      else { 
          [loadingRequest finishLoadingWithError:err]; 
          NSLog(@"bad key response"); 
      } 
      handled = YES; 
  bail: 
      return handled; 
       
  }
  ```

## Enable Apple FairPlay in TVSDK applications {#section_61CFA3C22FE64F52B2C8CE860B72E88B}

You can implement Apple FairPlay Streaming, which is Apple's DRM solution, in your TVSDK applications.

1. Create your FairPlay Customer Resource Loader by implementing `PTAVAssetResourceLoaderDelegate`. For more information, see Apple FairPlay in TVSDK applications.

   >[!NOTE]
   >
   >Ensure that you follow the instructions in the *FairPlay Streaming Program Guide* ( *FairPlayStreaming_PG.pdf*), which is included in [FairPlay Server SDK for Developing a FPS-Aware App](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   The method `resourceLoader:shouldWaitForLoadingOfRequestedResource` is equivalent to what is in `AVAssetResourceLoaderDelegate`. 

   >[!NOTE]
   >
   >In the ExpressPlay license server scenario, to play back content, change the URL scheme in your ExpressPlay FairPlay server license request URL from `skd://` to `https://` (or `https://`).

1. Register the *FairPlay* Customer Resource Loader with `registerPTAVAssetResourceLoader`. 

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

   >[!NOTE]
   >
   >If you wrote your own FairPlay license server, or you are using a third-party FairPlay license server, consult your license server vendor to determine your license server URL, formatting, and any other requirements.
