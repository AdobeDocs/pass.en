---
description: The TVSDK currently provides built-in ad provider metadata support for TVSDK ads, direct ad breaks, and custom ad markers.
title: Ad insertion types
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
---
# Ad insertion types {#ad-insertion-types}

The TVSDK currently provides built-in ad provider metadata support for TVSDK ads, direct ad breaks, and custom ad markers.

It supports the following types of ad insertion workflows for VOD and live/linear content. 

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Insertion type </th> 
   <th colname="col2" class="entry"> Supported in... </th> 
   <th colname="col3" class="entry"> Description </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime ad decisioning ads </td> 
   <td colname="col2">VOD <p>Live </p> <p>Linear </p> </td> 
   <td colname="col3">The reference implementation provides <span class="codeph"> AuditudeMetadata</span> information to connect to the server for Primetime ad decisioning (previously known as Auditude), based on the information provided in the Primetime ads portion</a> of the JSON configuration file</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Direct ad breaks </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">You must provide ad URLs in the input JSON file. When the TVSDK attempts to resolve an ad, it calls the direct ad break resolver and resolves the ads based on the direct ad breaks information provided in the JSON configuration file</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Custom ad markers </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Custom ad markers are useful when the video stream contains both main content and ads but does not include information related to the ad positions and timing. If the ad positioning information is obtained in another way, for example, through an external CMS, you can define custom ad markers and pass them to the player timeline. <p>To set up a player for ad insertion, you need to pass ad metadata in the custom ad metadata section of the JSON configuration file</a>, which has a supporting ad provider implementation in the reference implementation. </p> </td>
  </tr>
 </tbody>
</table>
