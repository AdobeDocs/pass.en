---
title: Device capabilities required to play protected content
description: Device capabilities required to play protected content
copied-description: yes
exl-id: 540fbb53-ec1a-43be-b51b-9937ed31e384
---
# Device capabilities required to play protected content {#device-capabilities-required-to-play-protected-content}

Device capabilities required specifies the hardware capabilities required to access content. Information about the hardware capabilities is available for devices that use the porting kit.

The following attributes can identify the device capabilities: 

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Attribute</b> </td> 
   <td><b>Supported Values</b> </td> 
   <td><b>Match Criteria</b> </td> 
   <td><b>Description</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Non-user accessible bus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true” or “false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exact Match </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">If true, device must not have a user-accessible bus. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Hardware root of trust </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true” or “false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exact Match </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">If true, device must have a hardware root of trust. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>This usage rule is supported by Adobe Primetime DRM clients version 2.0.2 and later. The behavior on older clients depends on the minimum client version supported by the license server. 
>
>See [Minimum Client Version](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
