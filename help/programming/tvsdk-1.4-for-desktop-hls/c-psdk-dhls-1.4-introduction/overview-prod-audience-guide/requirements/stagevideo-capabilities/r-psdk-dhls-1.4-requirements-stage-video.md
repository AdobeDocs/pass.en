---
description: On devices that support GPU (hardware) acceleration, you can use a flash.media.StageVideo object to process video directly on the device hardware.
title: StageVideo minimum requirements
exl-id: f401682d-c47d-4284-8832-293515a76581
---
# StageVideo minimum requirements{#stagevideo-minimum-requirements}

On devices that support GPU (hardware) acceleration, you can use a flash.media.StageVideo object to process video directly on the device hardware.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

A combination of different factors determine when and how you can use `StageVideo`. The following table presents a snapshot of some of the requirements and restrictions that are associated with using StageVideo. These requirements and restrictions are subject to change. 

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Platform </th> 
   <th colname="col2" class="entry"> Windows and Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">At least Flash 10.1 or later </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">For the fallback to software feature, Flash 15 and later </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Browsers and <span class="codeph"> wmode</span> settings </td> 
   <td colname="col2"> <p><b>On Flash 15</b>, set <span class="codeph"> wmode=opaque</span> so you can use HTML overlays. </p> <p>The following browsers currently do not support hardware acceleration: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox on Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome before 26 and any version of Chrome on Windows XP and Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (all versions) </li> 
     </ul>Other browser/OS combinations might prevent access to hardware acceleration. In these scenarios, <span class="codeph"> StageVideo</span> falls back to software with a negative impact on performance. </p> <p><b>On Flash 14 and earlier</b>, if the browser does not support hardware acceleration, the Flash player can render directly to the GPU, but set <span class="codeph"> wmode=direct</span> to enable this rendering. <p>Tip:  GPU drivers that are older than 2009 might need to be updated as these drivers might lack support for hardware acceleration. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream object </td> 
   <td colname="col2">The <span class="codeph"> StageVideoEvent.RENDER_STATE</span> event is not dispatched unless you attach a <span class="codeph"> NetStream</span> object to the <span class="codeph"> StageVideo</span> object. </td> 
  </tr> 
 </tbody> 
</table>
