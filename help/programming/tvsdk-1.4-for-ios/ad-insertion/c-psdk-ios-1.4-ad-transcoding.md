---
description: Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.
title: Repackage incompatible ads using Adobe Creative Repackaging Service
exl-id: 6766bdf7-bffb-4dc1-bc8d-148a7f713f5f
---
# Repackage incompatible ads using Adobe Creative Repackaging Service{#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Some third-party ads (or creatives) cannot be stitched into the HTTP Live Streaming (HLS) content stream because their video format is incompatible with HLS. Primetime ad insertion and TVSDK can optionally attempt to repackage incompatible ads into compatible M3U8 videos.

Ads served from various third parties, such as an agency ad server, your inventory partner, or an ad network, are often delivered in incompatible formats, such as progressive-download MP4.

When TVSDK first encounters an incompatible ad, the player ignores the ad and issues a request to the creative repackaging service (CRS), which is part of the Primetime ad insertion back end, to repackage the ad into a compatible format. CRS attempts to generate multiple-bit-rate M3U8 renditions of the ad and stores these renditions on the Primetime Content Delivery Network (CDN). The next time TVSDK receives an ad response that points to that ad, the player uses the HLS-compatible M3U8 version from the CDN.

To enable this optional feature, contact your Adobe representative.

For more information about CRS, see [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Multiple CDN support for CRS ad delivery {#section_900FDDA5454143718F1EB4C9732C8E1C}

While the default Creative Repackaging Service (CRS) scenario is to use one Content Data Network (CDN), you can deploy CRS assets on more than one CDN.

You can use multiple CDNs for the following reasons:

* A requirement to scale up for large viewing events. 
* A requirement to match the CDN source of the CRS asset with the CDN source of the main content.

You can transform the default URL that is provided by the CRS by using TVSDK URL Transformer APIs.

Here are the API additions in TVSDK:

* `PTURLTransformer` A protocol that describes the methods that are required to transform the CRS ad URLs that are requested by TVSDK. Applications can implement this protocol and provide implementations for the required methods. 

* `PTDefaultURLTransformer` The default URL transformer instance that is created in TVSDK and that implements the `PTURLTransformer` protocol. Applications can override this class or add a post URL transformation handler. This handler is useful when the application wants to make changes to the URL request after the default transformation has been applied. 

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` A setter method that is provided on the `PTNetworkConfiguration` metadata instance to set the `PTURLTransformer` implementation.

>[!IMPORTANT]
>
>Your app implementations must check for the `PTURLTransformerInputType` enumeration and only transform URLs of type `PTURLTransformerInputTypeCRSCreative` for CRS.

The following code sample shows how your application can change the default host component to a different string (for example, `cdn.mycrsdomain.com`): 

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
