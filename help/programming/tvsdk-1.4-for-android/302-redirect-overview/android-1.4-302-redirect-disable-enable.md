---
description: 302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.
title: Disable or enable 302 redirect optimization
exl-id: b1bdb6d6-b34d-4e0a-8c96-7fd4ce77b5c9
---
# HTTP 302 redirect optimization {#http-302-redirect-optimization}

302 redirect optimization minimizes the number of 302 redirect responses, which allows your application to load balance more effectively.

If a main manifest request is redirected, and 302 optimization is enabled in your player, subsequent requests made for assets from that manifest will use the final domain location, which avoids additional 302 responses.

This feature is enabled by default, and you can change this setting.

## Disable or enable 302 redirect optimization{#disable-or-enable-redirect-optimization}

Use the `useRedirectedUrl` property to turn 302 redirect on (true) or off (false). 
For example: 

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```
