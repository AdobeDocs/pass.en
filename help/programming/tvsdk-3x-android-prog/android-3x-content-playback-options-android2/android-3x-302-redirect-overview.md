---
description: 302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.
title: HTTP 302 redirect optimization
exl-id: a238e90f-3aa1-486b-b57f-d543e4c94b2e
---
# HTTP 302 redirect optimization {#http-redirect-optimization}

302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.

 If a main manifest request is redirected, and 302 optimization is enabled in your player, subsequent requests made for assets from that manifest will use the final domain location, which avoids additional 302 responses. This feature is enabled by default, and you can change this setting.

## Disable or enable 302 redirect optimization {#section_8977448B268E41D69A8F75B60EB9DA3B}

Use the `useRedirectedUrl` property to turn 302 redirect on ( `true`) or off ( `false`).

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

For example: 

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
