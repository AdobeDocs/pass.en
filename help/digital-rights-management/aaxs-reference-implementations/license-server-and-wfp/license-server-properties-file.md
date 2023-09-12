---
title: License server properties file
description: License server properties file
copied-description: yes
exl-id: ac105ea6-b5a4-4416-bf17-f619abcf7cd5
---
# License server properties file {#license-server-properties-file}

Use the [!DNL flashaccess-refimpl.properties] file to configure the License Server component of the reference implementation. At a minimum, be sure to configure the properties related to the Transport Credential and the License Server Credential. The locations of the credential files must be specified relative to the directory specified by the `config.resourcesDirectory` property. This file also contains several properties related to packaging content: these properties are only used for Flash Media Rights Management Server 1.x metadata conversion. If you modify any of the values in this property file, you need to restart the license server for the changes to take effect.

To support generation of licenses for Remote Key delivery to iOS clients in Adobe Access, the Key Server certificate must be specified in [!DNL flashaccess-refimpl.properties].

The following properties have been added in Adobe Access: 

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
   <td colname="2" class="- topic/entry "> Key Server's License Server Certificate, issued by Adobe. This certificate is used to generate licenses for iOS devices, when the metadata indicates that a Key Server is required. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Alias of Key Server's Adobe-issued License Server certificate stored on HSM. When HSM is enabled, use this property instead of <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
