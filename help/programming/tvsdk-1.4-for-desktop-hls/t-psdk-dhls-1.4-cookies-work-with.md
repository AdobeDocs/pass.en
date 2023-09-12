---
description: You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.
title: Work with cookies
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
---
# Work with cookies{#work-with-cookies}

You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.

Here is a example with some type of authentication when making requests to the key server:

1. Your customer logs into your website in a browser and their login shows that they are allowed to view content. 
1. Your application generates an authentication token, based on what is expected by the license server. Pass that value to TVSDK. 
1. TVSDK sets that value in the cookie header. 
1. When TVSDK makes a request to the key server to get a key to decrypt the content, that request contains the authentication value in the cookie header, so the key server knows that the request is valid.

To work with cookies: 

1. Use the `cookieHeaders` property in `NetworkConfiguration` to set a cookie. The `cookieHeaders` property is a Metadata object, and you can add key value pairs to this object to be included in the cookie header.

   For example:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
     
   networkConfiguration.cookieHeaders = metadata;
   ```

   By default, cookie headers are sent only with key requests. To send cookie headers with all requests, set the `NetworkConfiguration` property `useCookieHeadersForAllRequests` to true. 

1. To ensure that `NetworkConfiguration` works, set it as metadata:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Provide the metadata from the previous step when you create a `MediaResource`.

   For example, if you use the `createFromURL` method, enter the following information: 

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
