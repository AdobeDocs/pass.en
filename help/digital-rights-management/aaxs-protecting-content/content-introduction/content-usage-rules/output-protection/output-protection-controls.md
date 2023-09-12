---
title: Output protection controls
description: Output protection controls
copied-description: yes
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
---
# Output protection controls {#output-protection-controls}

**Control whether output to external rendering devices is protected. Specify analog and digital outputs independently.**

Controls whether output to external rendering devices should be restricted. An external device is defined as any video or audio device that is not embedded in the computer. The list of external devices excludes integrated displays, such as in notebook computers. Analog and digital output restrictions can be specified independently.

The following options/levels of enforcement are available: 

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Supported in analog devices </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Supported in digital devices </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Required</b> — Analog Copy Protection (ACP) or Copy Generation Management System - Analog (CGMS-A) output protection must be enabled in order to play content to an external device. Adobe Access clients must enable output protection using ACP or CGMS-A. On devices that support both, the Adobe Access 3.0 clients will attempt to enable both. However, only one must be enabled to play the content. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP Required</b> — ACP output protection is required. Playback is not allowed on CGMS-A. Adobe Access 2.0 clients do not support this option. If set, an Adobe Access 2.0 client will behave as if the “No Playback” option was specified. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A Required</b> — CGMS-A output protection is required. Playback is not allowed on ACP. Adobe Access 2.0 clients do not support this option. If set, an Adobe Access 2.0 client will behave as if the “No Playback” option was specified. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use if available</b> — Attempt to enable ACP and CGMS-A output protection if available and allow playback if not available. Adobe Access 3.0 clients will attempt to enable both ACP and CGMS-A, if possible. Adobe Access 2.0 clients will only attempt to enable either ACP or CGMS-A. For instance, an attempt will be made by the Adobe Access client to enable either ACP or CGMS-A. If the attempt succeeds, the other option will not be enabled. If the attempt fails, a second attempt will be made to enable the other option. Even if both the attempts fail, the content will be played anyway. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use ACP if available</b> — Attempt to enable ACP output protection if available, but allow playback if not available. Protection is not available on CGMS-A. Adobe Access 2.0 clients do not support this option. If set, an Adobe Access 2.0 client will behave as if the “No Protection” option was specified. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use CGMS-A if available </b>— Attempt to enable CGMS-A output protection if available, but allow playback if not available. Protection is not available on ACP. Adobe Access 2.0 clients do not support this option. If set, an Adobe Access 2.0 client will behave as if the “No Protection” option was specified. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">No protection</b> — No output protection enablement is enforced for analog and digital outputs. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">No playback</b> —Do not allow playback to an external device for analog and digital outputs. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">YES </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>While these rules are consistently enforced across all platforms, currently it is only possible to securely turn on output protection on Windows platforms. On other platforms (such as Macintosh and Linux) there are no supporting operating system functions available to third party applications.

Example use case: Some content might enforce output protection controls, and the level of protection can be set by the content distributor. If “Required” is specified and playback is attempted on a Macintosh, the client does not play back content on external devices. The content will, however, play back on internal monitors.

If “Required” is specified and playback is attempted on Linux, the client does not play back content on any devices because it is not possible to differentiate between internal and external devices.

If you specify “Use if available”, output protection is turned on where possible. For example, on Windows machines that support the Certified Output Protection Protocol (COPP), the content is passed with output protection to an external display. This example is sometimes known as “selectable output control”.
