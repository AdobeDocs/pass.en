---
description: 302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.
title: HTTP 302 redirect optimization
exl-id: 9b9d98ae-a509-47dc-a5ac-6be9b0f214c1
---
# HTTP 302 redirect optimization{#http-redirect-optimization}

302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.

 If a main manifest request is redirected, and 302 optimization is enabled in your player, subsequent requests made for assets from that manifest will use the final domain location, which avoids additional 302 responses.

This feature is disabled by default, and you can change this setting.

If you enable this feature, it works correctly only if *all* of the following conditions are true; otherwise, no redirect optimization occurs, and 302 responses continue to occur:

* Your application was compiled for Adobe Flash Player 11.8, using `-swf-version` 21 or higher. 
* Your end users have Adobe Flash Player 11.8 or later installed.

>[!IMPORTANT]
>
>To ensure that cookies are passed with ad requests, disable 302 redirect. When 302 redirect is enabled, the ad request might be redirected to a domain that is different from the domain from which the cookie originated.

## Disable or enable 302 redirect optimization {#section_D6687FC44C61446F878008B629A5FA19}

Use the `useRedirectedUrl` property to turn 302 redirect on (true) or off (false).

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

For example: 

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```
