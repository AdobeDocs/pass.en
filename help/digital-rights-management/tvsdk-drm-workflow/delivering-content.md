---
title: Delivering content
description: Delivering content
copied-description: yes
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
---
# Delivering content {#delivering-content}

Primetime DRM is agnostic to the delivery mechanism of the content as the runtime abstracts out the networking layer and simply provides the protected content to the Primetime DRM subsystem. Hence, content can be delivered through HTTP, HTTP Dynamic Streaming, RTMP, or RTMPE, HLS, etc.

However, depending on the protocol, there may be intricacies involved with retrieving the protected content's metadata ( `DRMContentData` - usually in the form of a side-loaded [!DNL .metadata] file). This DRM metadata is required to call any `DRMManager` API, such as pre-fetching the license, DRM authentication, or joining a device domain. For example, with the RTMP/RTMPE protocol, only FLV and F4V data can be delivered to the client through the Flash Media Server (FMS). Because of this, the client must retrieve the metadata blob by other ways. One option to solve this problem is to host the metadata on an HTTP web server, and implement the client video player to retrieve the appropriate metadata, depending on the content being played back. 

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 

```
