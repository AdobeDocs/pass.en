---
description: TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.
title: Companion banner ads
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
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

The content of an AdBannerAsset describes a companion banner.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

The `AdPlaybackEvent.AD_STARTED` event returns an `Ad` instance that contains a `companionAssets` property ( `Vector.<AdAsset>`). 
Each `AdAsset` provides information about displaying the asset. 

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
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> banner data </td> 
   <td colname="col2"> The data of the type that is specified by <span class="codeph"> resourceType</span> for this companion banner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> static URL </td> 
   <td colname="col2"> <p>Sometimes, the companion banner also has a staticURL that is a direct URL to the image or to a <span class="filepath"> .swf</span> (flash banner). </p> <p>If you do not want to use html or iframe, you can use a direct URL to an image or swf to display the banner in the Flash stage instead. In this case, you can use the staticURL to display the banner. </p> <p>Important:  You must check whether the static URL is a valid string, because this property might not always be available. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Display banner ads {#display-banner-ads}

To display banner ads, you need to create banner instances and allow TVSDK to listen for ad-related events.

TVSDK provides a list of companion banner ads that are associated with a linear ad through the `AdPlaybackEvent.AD_STARTED` event event.

Manifests can specify companion banner ads by:

* An HTML snippet 
* The URL of an iFrame page 
* The URL of a static image or an Adobe Flash SWF file

For each companion ad, TVSDK indicates which types are available for your application. 

  Add a listener for the `AdPlaybackEvent.AD_STARTED` event that does the following:

   1. Clears existing ads in the banner instance.

   1. Gets the list of companion ads from `Ad.companionAssets`.

   1. If the list of companion ads is not empty, iterate over the list for banner instances.

      Each banner instance ( an `AdBannerAsset`) contains information, such as width, height, resource type (html, iframe, or static), and data that is required to display the companion banner.

   1. If a video ad has no companion ads booked with it, the list of companion assets contains no data for that video ad.
   
      To show a standalone display ad, add the logic to your script to run a normal DFP (DoubleClick for Publishers) display ad tag in the appropriate banner instance.

   1. Sends the banner information to a function on your page  ,usually JavaScript, by using `ExternalInterface`,  that displays the banners in an appropriate location.

      This is usually a `div`, and your function uses the `div ID` to display the banner. For example:

      Add the event listener:

      ```js
      _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
      ```

      Implement the listener handler:    
   
      ```js   
      private function onAdStarted(event:AdPlaybackEvent):void { 
          // check if there are any companion banner 
          if (event.ad && event.ad.companionAssets  
                       && event.ad.companionAssets.length > 0) { 
              for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
                  if (ExternalInterface.available) { 
                      //-- call the java script that will handle the banner display. 
                      ExternalInterface.call('addBanner', banner.resourceType,  
                          banner.width, banner.height, banner.bannerData); 
                  } 
              } 
          }  
          //...        
      }
      ```

      Example of JavaScript to handle the display:    
   
      ```js   
      function addBanner(resourceType, width, height, data) { 
          console.log(resourceType + "," +  width + "," +  height); 
       
      //Assume an html element on the page with id like 'banner300x250' 
          var bannerDiv = document.getElementById('banner' + width +  
              'x' + height);  
          if (bannerDiv != null) { 
              if (resourceType == "html") { // for html resource 
                  bannerDiv.innerHTML = data; 
              } 
              else if (resourceType == "iframe") { // for iframe resource 
                  bannerDiv.innerHTML = "<iframe src='" + data +  
                      "' width='100%' height='100%'></iframe>"; 
              } 
          } 
      }
      ```
