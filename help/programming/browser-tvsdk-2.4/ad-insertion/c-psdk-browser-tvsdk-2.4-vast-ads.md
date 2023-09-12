---
description: When Browser TVSDK requests an ad that is not on your primary ad server, the player needs to request the ad from the secondary server. Video Ad Serving Template (VAST) sets the standard of communication between ad servers and video players and is the response that is sent by the secondary ad server when the ad is requested.
title: VAST ads
exl-id: b0ebade5-b5da-413d-84f4-abebac579f45
---
# VAST ads {#vast-ads}

When Browser TVSDK requests an ad that is not on your primary ad server, the player needs to request the ad from the secondary server. Video Ad Serving Template (VAST) sets the standard of communication between ad servers and video players and is the response that is sent by the secondary ad server when the ad is requested.

For more information about VAST, see [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

Browser TVSDK supports the following VAST ad elements:

## Wrapper and inline ads {#section_11B8A1A8F52F4F77981C6AAC02185087}

The following elements are supported:

* **`wrapper`** When the player needs to contact a secondary ad server to request an ad, the wrapper element provides the redirect information. One wrapper element can point to several wrappers that ultimately point to a VAST ad.

* **`inline`** The following required elements are supported:

* `AdSystem`
* `AdTitle`
* `Impression`

  The following optional elements are supported:

* `Description`
* `Survey`
* `Error`

## Creatives {#section_0121F948CB074E49A8132D202786CAA4}

This element is a file that is a part of a VAST ad and contains a `creative` element that can support a linear ad, a non-linear ad, or a companion ad. In the `creative` element, the `id`, `sequence`, and `adId` elements are supported.

Here is more information about the ad types:

* **Linear ads** The following elements are supported:

  * `TrackingEvent`, which contains the `Tracking` element.
    * `Duration`
    * `AdParameters`
    * `VideoClicks`, including the following:

    * `ClickThrough`
    * `ClickTracking`
    * `CustomClick`

    * `MediaFiles`

    * `MediaFile`

      >[!TIP]
      >
      >In this element, the `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`, and `type` attributes are supported.

* **Non-Linear ads** The following elements are supported:

  * `Non-linear`

    >[!TIP]
    >
    >In this element, the `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`, and `minSuggestedDuration` attributes are supported.

    * `StaticResource`
    * `IFrameResource`
    * `HTMLResource`
    * `NonLinearClickThrough`
    * `AdParameters`

* **Companion ads** The following elements are supported:

  * `Companion`
    
    >[!TIP]
    >
    >In this element, the `id`, `width`, `height`, `apiFramework`, `expandedWidth`, and `expandedHeight` attributes are supported.

    * `StaticResource`
    * `IFrameResource`
    * `HTMLResource`
    * `TrackingEvents`

## Extensions {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Only Auditude-specific extensions are supported.

* `Extension`
