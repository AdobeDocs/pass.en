---
description: 302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.
title: HTTP 302 redirect optimization
exl-id: 80d5d38d-c998-4fc0-b527-b38e578d76e7
---
# HTTP 302 redirect optimization {#http-redirect-optimization}

302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.

 If a main manifest request is redirected, and 302 optimization is enabled in your player, subsequent requests made for assets from that manifest will use the final domain location, which avoids additional 302 responses. This feature is enabled by default, and you can change this setting.

>[!IMPORTANT]
>
>This feature is supported only in the certified browsers that support the `responseURL` property in the `XMLHttpRequest` object.

For Flash fallback, remember the following information:

* Your end users must have Adobe Flash Player version 23 or later installed. 
* If stream integrity is disabled, 302 redirect is supported on certified browsers only.

## Disabling 302 redirect optimization {#disabling-redirect-optimization}

You can use the useRedirectedUrl property to enable 302 redirect (true) or disable (false).

For example: 

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
