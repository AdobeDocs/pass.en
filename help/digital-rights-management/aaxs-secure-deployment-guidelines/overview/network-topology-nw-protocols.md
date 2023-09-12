---
title: Network protocols used by Adobe Access
description: Network protocols used by Adobe Access
copied-description: yes
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
---
# Network protocols used by Adobe Access {#network-protocols-used-by-adobe-access}

When you configure a secure network architecture, the network protocols in the following table are required for interaction between Adobe Access and other systems in your enterprise network. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocol </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player , Adobe AIR®, and Adobe Primetime clients communicate with Adobe Access over HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (Optional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR, and Adobe Primetime clients can use HTTPS for communication with Adobe Access, however, HTTPS (SSL) is not required unless you need support for FMRMS 1.x clients. See the notes in the table <a href="network-topology-firewall-rules.md" format="dita" scope="local"> Incoming URLs</a> and <a href="network-topology-nw-protocols.md"> Configuring SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
