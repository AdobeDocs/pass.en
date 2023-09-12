---
description: For Digital Video Ad Serving Template (VAST) ads (or creatives) that have the fallback rule enabled, TVSDK treats an ad with an invalid media type as an empty ad and attempts to use fallback ads in its place. You can configure some aspects of fallback behavior.
title: Ad fallback for VAST and VMAP ads
exl-id: 5c469686-f8db-463a-ad1a-cb64e9192fb7
---
# Ad fallback for VAST and VMAP ads {#ad-fallback-for-vast-and-vmap-ads}

For Digital Video Ad Serving Template (VAST) ads (or creatives) that have the fallback rule enabled, TVSDK treats an ad with an invalid media type as an empty ad and attempts to use fallback ads in its place. You can configure some aspects of fallback behavior.

The VAST/Digital Video Multiple Ad Playlist (VMAP) specification states that for ads where VAST fallback is enabled, empty ads automatically trigger the use of fallback ads. When a VAST ad is empty, TVSDK looks for a valid HLS media type replacement among the fallback ads. When a VAST ad in a wrapper has an invalid media type, TVSDK treats this ad as empty. You can configure whether TVSDK should do the same for ads inline in a VMAP. For more information about the VAST `fallbackOnNoAd` feature, see [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Define fallback ad behavior for VMAP inline ads {#section_D90BB3C6E539472EABF000C0F616DBE2}

You can turn on fallback when a VMAP inline ad contains an invalid media type.

1. Set `FallbackOnInvalidCreativeEnabled` to `YES` to have VMAP fall back when the media type for a linear/inline ad is invalid for HLS. 

   >[!NOTE]
   >
   >The default value is NO. If a linear ad fails because it is has an invalid media type, or because the ad cannot be repackaged, this flag allows Primetime ad decisioning to follow the same fallback behavior as if the ad was an empty VAST wrapper.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Ad fallback behavior for VAST and VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

When Primetime ad decisioning encounters a VAST ad (creative) that is empty or that has a media type that is invalid for HLS, it evaluates the fallback ads to determine what to return.

In TVSDK, the only valid media type is `application/x-mpegURL` (M3U8).

When there are stand-alone fallback ads, the Primetime ad decisioning plug-in looks examines these ads in the following order and returns the first ad with a valid media type:

1. If repackaging is enabled, the first occurrence of an ad with an invalid media type is treated like other invalid media types.

   If repackaging fails, this process applies to additional occurrences of the ad. 
1. If TVSDK finds no valid fallback ads, it returns the original ad with the invalid media type. 
1. If a fallback ad with a valid MIME type is returned instead of the original ad, Primetime ad decisioning sends error code 403 to the VAST error URL, if available. 
1. If a fallback ad is a wrapper and returns multiple ads, only ads with the correct media type are returned.

>[!IMPORTANT]
>
>This behavior is always enabled for ads in VAST wrappers. For VAST ads inline in a VMAP, the behavior is disabled by default, but your application can enable it.
