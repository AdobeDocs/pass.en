---
description: Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.
title: Repackage incompatible ads using Adobe Creative Repackaging Service
exl-id: 8c3e5baf-1941-4330-a4b7-61ed623dfd5e
---
# Repackage incompatible ads using Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.

Ads served from various third parties, such as an agency ad server, your inventory partner, or an ad network, are often delivered in incompatible formats, such as progressive-download MP4.

When TVSDK first encounters an incompatible ad, the player ignores the ad and issues a request to the creative repackaging service (CRS), which is part of the Primetime ad insertion back end, to repackage the ad into a compatible format. CRS attempts to generate multiple-bit-rate M3U8 renditions of the ad and stores these renditions on the Primetime Content Delivery Network (CDN). The next time TVSDK receives an ad response that points to that ad, the player uses the HLS-compatible M3U8 version from the CDN.

To enable this optional feature, contact your Adobe representative.

For more information about CRS, see [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Multiple CDN support for CRS ad delivery{#multiple-cdn-support-for-crs-ad-delivery}

While the default Creative Repackaging Service (CRS) scenario is to use one Content Data Network (CDN), you can deploy CRS assets on more than one CDN.

You can use multiple CDNs for the following reasons:

* A requirement to scale up for large viewing events. 
* A requirement to match the CDN source of the CRS asset with the CDN source of the main content.

You can transform the default URL that is provided by the CRS by using TVSDK URL Transformer APIs.

Here are the API additions in TVSDK:

* `URLTransformer` An interface that describes the methods that are required to transform the CRS ad URLs that are requested by TVSDK. Applications can implement this interface and provide implementations for the required methods. 

* `DefaultURLTransformer` The default URL transformer instance that is created in TVSDK and that implements the `URLTransformer` interface. Applications can override this class or add a post URL transformation handler. This handler is useful when the application wants to make changes to the URL request after the default transformation has been applied. 

* `NetworkConfiguration.setURLTransformer` A setter method that is provided on the `NetworkConfiguration` metadata instance to set the `URLTransformer` implementation.

>[!IMPORTANT]
>
>Your app implementations must check for the `URLTransformerInputType` enumeration and only transform URLs of type `URLTransformerInputType.CRSCreative` for CRS.

The following code sample shows how your application can change the default host component to a different string (for example, `cdn.mycrsdomain.com`): 

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
