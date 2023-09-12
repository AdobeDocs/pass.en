---
description: You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.
title: Work with cookies
exl-id: 7482777a-c338-4e0d-b123-ce2712657b8d
---
# Work with cookies{#work-with-cookies}

You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.

Here is a example with some type of authentication when making requests to the key server:

1. Your customer logs into your website in a browser and their login shows that they are allowed to view content. 
1. Your application generates an authentication token, based on what is expected by the license server. Pass that value to TVSDK. 
1. TVSDK sets that value in the cookie header. 
1. When TVSDK makes a request to the key server to get a key to decrypt the content, that request contains the authentication value in the cookie header, so the key server knows that the request is valid.

To work with cookies: 

1. Create a `cookieManager` and add your cookies for the URIs to your `cookieStore`.

   For example: 

   >[!IMPORTANT]
   >
   >When 302 redirect is enabled, the ad request may be redirected to a domain that is different from the domain to which the cookie belongs.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK queries this cookieManager at runtime, checks whether there are any cookies associated with the URL, and uses those automatically.

   Another option is to use `cookieHeaders` in `NetworkConfiguration` to set an arbitrary cookie header string to be used for requests. By default, this cookie header is sent only with key requests. To send the cookie header with all requests, use the `NetworkConfiguration` method `setUseCookieHeadersForAllRequests`: 

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
