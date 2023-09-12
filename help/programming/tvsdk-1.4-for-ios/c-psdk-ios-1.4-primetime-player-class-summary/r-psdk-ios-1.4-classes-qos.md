---
description: These classes provide information that help you to determine how well the player is performing.
title: QoS classes
exl-id: ba0cddd0-3af9-4e35-9079-97c260cbd3e9
---
# QoS classes{#qos-classes}

These classes provide information that help you to determine how well the player is performing.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Name </th> 
   <th colname="2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">Provides information about the platform and operating system on which the TVSDK runs: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Version of the platform OS </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Version number of the TVSDK library </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Device's model name </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Device manufacturer's name </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">Dehvice UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Width/height of the device screen </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> Provides information on how the playback is performing. This includes the frame rate, the profile bit rate, the total time spent in buffering, the number of buffering attempts, the time it took to get the first byte from the first video fragment, the time it took to render the first frame, the currently buffered length, and the buffer time. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      Provides essential QoS metrics for both playback and the device.
    </pre>
    <pre>
      QOS information provider class.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
