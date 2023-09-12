---
description: TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.
title: Companion banner ads
exl-id: e7b0ce38-e4b0-4e10-8d76-2d43d8eff665
---
# Companion banner ads {#companion-banner-ads}

TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.

When displaying companion ads, follow these recommendations:

* Attempt to present as many of a video ad's companion banner ads as will fit in your player's layout. 
* Present a companion banner only if you have a location that exactly matches its specified height and width. 

  >[!TIP]
  >
  >Do not resize the banner.

* Present the companion banner(s) as soon as possible after the ad begins. 
* Do not overlay the main ad/video container with companion banners. 
* Continue to display companion banners after the ad ends.

  The standard is to display each companion banner until you have a replacement for this banner.

## Companion banner data {#companion-banner-data}

The content of a PTAdAsset describes a companion banner.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

The `PTMediaPlayerAdStartedNotification` notification returns a `PTAd` instance that contains a `companionAssets` property (array of `PtAdAsset`). 
Each `PtAdAsset` provides information about displaying the asset. 

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Available information </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Width of the companion banner in pixels. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Height of the companion banner in pixels. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> resource type </td> 
   <td colname="col2">The resource type for this companion banner: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: The data is in HTML code. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: The data is an iframe URL (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">static: The data is a staticURL that is a direct URL to an image. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> The data of the type that is specified by <span class="codeph"> resourceType</span> for this companion banner. </td> 
  </tr> 
 </tbody> 
</table>

## Display banner ads {#display-banner-ads}

To display banner ads, you need to create banner instances and allow TVSDK to listen for ad-related events.

TVSDK provides a list of companion banner ads that are associated with a linear ad through the `PTMediaPlayerAdPlayStartedNotification` notification event.

Manifests can specify companion banner ads by:

* An HTML snippet 
* The URL of an iFrame page 
* The URL of a static image or an Adobe Flash SWF file

For each companion ad, TVSDK indicates which types are available for your application. 

1. Create  a `PTAdBannerView`  instance for each companion ad slot on your page.

       Ensure that the following information has been provided:

    * To prevent the retrieval of companion ads of different sizes, a banner instance that specifies the width and height. 
    * Standard banner sizes.

1. Add an observer for the `PTMediaPlayerAdStartedNotification` that does the following:
   1. Clears existing ads in the banner instance.
   1. Gets the list of companion ads from `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. If the list of companion ads is not empty, iterate over the list for banner instances.
   
      Each banner instance ( a `PTAdAsset`) contains information, such as width, height, resource type (html, iframe, or static), and data that is required to display the companion banner.   
   1. If a video ad has no companion ads booked with it, the list of companion assets contains no data for that video ad.
   
      To show a standalone display ad, add the logic to your script to run a normal DFP (DoubleClick for Publishers) display ad tag in the appropriate banner instance.   
   1. Sends the banner information to a function on your page that displays the banners in an appropriate location.
   
      This is usually a `div`, and your function uses the `div ID` to display the banner. For example:

      ```   
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
       
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
       
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
       
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
