---
description: Support for the withCredentials attribute in XMLHttpRequests allows cross-origin resource sharing (CORS) requests to include the target domain's cookies for a variety of request types.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
title: Cross-origin resource sharing
exl-id: 02826c87-b0c6-495b-a17d-67c5693a9772
---
# Cross-origin resource sharing {#cross-origin-resource-sharing}

Support for the withCredentials attribute in XMLHttpRequests allows cross-origin resource sharing (CORS) requests to include the target domain's cookies for a variety of request types.

When the client requests a manifest, segment, or key, the server may set a cookie that the client must pass for subsequent requests. To allow for reading and writing cookies, the client must set the `withCredentials` attribute to `true` for cross-origin requests.

To enable `withCredentials` support for most types of requests when playing a given media resource: 

1. Create the `CORSConfig` object.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Attach the `corsConfig` to the `NetworkConfiguration` object and set `useCookieHeaderForAllRequests` to `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Set `networkConfig` in the `MediaPlayerItemConfig` object.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Pass `MediaPlayerItemConfig` to the `MediaPlayer.replaceCurrentResource` method.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
    
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   
   ```

>[!IMPORTANT]
>
>The `useCookieHeaderForAllRequests` flag does not affect license requests. To set the `withCredentials` attribute to `true` for a license request, you must set the `withCredentials` attribute in your protection data or specify an authorization key in the `httpRequestHeaders` of your protection data. For example: 

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

The flag does not affect a license request because some servers set the `Access-Control-Allow-Origin` field to wildcard ('&#42;') in their response. But, when the credentials flag is set to `true`, the wildcard cannot be used in `Access-Control-Allow-Origin`. If you set `useCookieHeaderForAllRequests` to `true` for all types of requests, you might see the following error for a license request:  

Remember the following information:

* When a call with `withCredentials=true` fails, Browser TVSDK retries the call without `withCredentials`.
* When a call is made with `networkConfiguration.useCookieHeaderForAllRequests=false`, XHR requests are made without the `withCredentials` attribute.
