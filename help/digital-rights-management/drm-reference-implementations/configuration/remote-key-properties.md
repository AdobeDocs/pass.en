---
title: Remote key delivery properties (iOS)
description: Remote key delivery properties (iOS)
copied-description: yes
exl-id: 0fe3ed9b-a8ee-43b4-ab3c-8ea2e696503b
---
# Remote key delivery properties (iOS){#remote-key-delivery-properties-ios}

To support the generation of licenses for Remote Key delivery to an iOS client in Adobe Primetime DRM , you must specify the Key Server certificate in the `flashaccess-refimpl.properties` file.

The following properties have been added in Primetime DRM : 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Property </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Key Server's License Server Certificate that is issued by Adobe. </p> <p>This certificate generates licenses for iOS devices when the metadata indicates that a Key Server is required. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>The alias of a Key Server's Adobe-issued License Server certificate that is stored on HSM. </p> <p>When you enable HSM, you can apply this property instead of the <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> property. </p> </td> 
  </tr> 
 </tbody> 
</table>
