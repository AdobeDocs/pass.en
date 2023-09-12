---
description: These classes provide information about ads that occur within a timeline.
title: Timeline advertising classes
exl-id: 4411c86d-8c40-457b-bfc1-40fbea77154e
---
# Timeline advertising classes {#timeline-advertising-classes}

These classes provide information about ads that occur within a timeline.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Name</b></th> 
   <th colname="2" class="entry"><b>Description</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">Class that defines the Ad abstraction and holds all ad information. It is defined by a unique ID, a duration, and a MediaResourcdee. The MediaResource contains the URL where the actual ad content resides. 
    <pre>
      Represents a primary linear asset spliced into the content. It can optionally contain an array of companion assets that must be displayed along with the linear asset.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">Class that represents an asset to be displayed. 
    <pre>
      Represents an asset to be displayed.
    </pre> 
    <pre>
      Class representing an ad asset.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Displays a banner asset. Your application must create a new instance of this utility class, set the banner asset, and add it to a view. The impression and click tracking for the banner is internally managed by this class.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">Class that gives a unified view on several ads that will be played at some point during playback. 
    <pre>
      Represents a continuous sequence of ads spliced into the content.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">Class that represents a click instance associated with an asset. This instance contains information about the click-through URL and the title that can be used to provide additional information to the user. 
    <pre>
      Represents a click instance associated with an asset. This instance contains information about the click-through URL and the title that can be used to provide additional information to the user.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protocol that defines properties for AdPolicySelector API calls. These properties provide the context for enforcing each ad behavior. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> An ad policy selector protocol for enforcing ad behaviors. Applications can conform to this protocol by implementing all the required methods or by extending the existing default policy selector class to customize specific behaviors. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> Class that represents the timeline of breaks within the content. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> class, 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> protocol
    </pre> </td> 
   <td colname="2"> Class that handles the ad-resolving part in the Adobe Primetime ad decisioning process. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protocol that describes the methods that the custom content resolver ( <span class="codeph"> PTContentResolver</span> ) should use to communicate to the delegate the status of the resolving of content. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">Class that abstracts a placement information request. Each resolved ad must have one placement information attached to it. The placement information describes where the ad is intended to be placed on the timeline. It contains information such as: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Placement position (in ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Type of the placement (pre-roll, mid-roll, or post-roll) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Duration of the main content chunk that is about to be replaced </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
