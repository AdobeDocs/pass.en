---
description: When you register event listeners with Browser TVSDK, you specify an event type to listen for and the name of your callback. When an event occurs, Browser TVSDK calls your callback and passes to it an event object of the appropriate type.
title: Event types and classes for callbacks
exl-id: 94c571ea-6dd2-4c15-89db-7015d89c9208
---
# Event types and classes for callbacks{#event-types-and-classes-for-callbacks}

When you register event listeners with Browser TVSDK, you specify an event type to listen for and the name of your callback. When an event occurs, Browser TVSDK calls your callback and passes to it an event object of the appropriate type.

<table frame="all" colsep="1" rowsep="1" id="table_FE58AD65AF3B4483816C00D7EAD2FB4F"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> When you listen for this event name (AdobePSDK.EventType) </th> 
   <th class="entry">phrases/browser-tvsdk-name passes an event to your callback of this object type (<span class="codeph"> AdobePSDK.Event</span>) </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_kj4_jc4_2y"> 
     <li id="li_C00AD7DE32C94431A4550E21CAC1DCA5"><span class="codeph"> AD_STARTED</span> </li> 
     <li id="li_1A3EA7527B3642E9ADF39F3CC3D87EDC"><span class="codeph"> AD_PROGRESS</span> </li> 
     <li id="li_9FB16D4B43EC4905909E881BC1C86E74"><span class="codeph"> AD_COMPLETED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> AdPlaybackEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_jpq_pc4_2y"> 
     <li id="li_782365D715684DDC835E16D08CC0BBDB"><span class="codeph"> AD_BREAK_STARTED</span> </li> 
     <li id="li_78D7EAEE99D04A35AD7C6EC60DDDC1CC"><span class="codeph"> AD_BREAK_COMPLETED</span> </li> 
     <li id="li_6155ADAF5E964C458E92AFFB4F7D6347"><span class="codeph"> AD_BREAK_SKIPPED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> AdBreakPlaybackEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> AD_CLICK</span> </td> 
   <td><span class="codeph"> AdClickEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_eny_tc4_2y"> 
     <li id="li_13F95E4BF905425CA5A95ECC138CC078"><span class="codeph"> BUFFERING_BEGIN</span> </li> 
     <li id="li_BA6F4E38E2F440FAAA4E70DF906A3350"><span class="codeph"> BUFFERING_END</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> BufferEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> DRM_METADATA_INFO_AVAILABLE</span> </td> 
   <td><span class="codeph"> DRMMetadataInfoAvailableEvent</span> </td> 
  </tr> 
  <tr> 
   <td colname="2"><span class="codeph"> LOAD_INFORMATION_AVAILABLE</span> </td> 
   <td><span class="codeph"> LoadInformationEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_kwy_cd4_2y"> 
     <li id="li_D5455D287EA5472D95A45AD1A8835D61"><span class="codeph"> AUDIO_UPDATED</span> </li> 
     <li id="li_AFF5B14338AB4AA8B4DF3963F2FDD4CF"><span class="codeph"> CAPTIONS_UPDATED</span> </li> 
     <li id="li_F7C9B933C6A44E80B57EB5274640A17B"><span class="codeph"> MASTER_UPDATED</span> </li> 
     <li id="li_C9FDF852BF4F4B638A8A1CAAFC27A23F"><span class="codeph"> ITEM_CREATED</span> </li> 
     <li id="li_85E13B35A6DB44A4BA0F93EA52B9D08A"><span class="codeph"> ITEM_UPDATED</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> MediaPlayerItemEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> STATUS_CHANGED</span> </td> 
   <td><span class="codeph"> StatusChangeEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> OPERATION_FAILED</span> </td> 
   <td><span class="codeph"> NotificationEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> RESERVATION_REACHED</span> </td> 
   <td><span class="codeph"> ReservationEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_jfl_224_2y"> 
     <li id="li_02B430978FA14A41A000DF8F9A345793"><span class="codeph"> RATE_SELECTED</span> </li> 
     <li id="li_1EDC0664B59E49448040DF312C928FAA"><span class="codeph"> RATE_PLAYING</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> PlaybackRateEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PROFILE_CHANGED</span> </td> 
   <td><span class="codeph"> ProfileEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PLAY_START</span> </td> 
   <td><span class="codeph"> PSDKEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> 
    <ul id="ul_nwg_w24_2y"> 
     <li id="li_7CABB2AD7AB140E3BD4061460987BA40"><span class="codeph"> SEEK_POSITION_ADJUSTED</span> </li> 
     <li id="li_D44BEC28BDBB408280F5AA77E06107B3"><span class="codeph"> SEEK_BEGIN</span> </li> 
     <li id="li_EC000CF7E3DF4BC18443E368E347E7ED"><span class="codeph"> SEEK_END</span> </li> 
    </ul> </td> 
   <td><span class="codeph"> SeekEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> SIZE_AVAILABLE</span> </td> 
   <td><span class="codeph"> SizeAvailableEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TIME_CHANGED</span> </td> 
   <td><span class="codeph"> TimeChangeEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_AVAILABLE</span> </td> 
   <td><span class="codeph"> TimedMetadataEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> TIMELINE_UPDATED</span> </td> 
   <td><span class="codeph"> TimelineEvent</span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"><span class="codeph"> PLAYBACK_RANGE_UPDATED</span> </td> 
   <td></td> 
  </tr> 
 </tbody> 
</table>
