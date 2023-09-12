---
title: Device capabilities required to play protected content
description: Device capabilities required to play protected content
copied-description: yes
exl-id: 5f2089e9-3176-46a7-9998-2dad0e77e453
---
# Device capabilities required to play protected content {#device-capabilities-required-to-play-protected-content}

Specifies the hardware capabilities required to access content. Information about the hardware capabilities is available for devices that use the porting kit.

The device capabilities may be identified by the attributes specified in the following table: 

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
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">If true, device must not have a user accessible bus. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Hardware root of trust </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">“true” or “false” </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exact Macth </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">If true, device must have a hardware root of trust. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>This usage rule is supported by Adobe Access clients version 2.0.2 and higher. The behavior on older clients depends on the minimum client version supported by the license server. See, [Minimum Client Version](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).
