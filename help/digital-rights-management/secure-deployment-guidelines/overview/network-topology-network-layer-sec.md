---
description: Network security vulnerabilities are among the first threats to any Internet-facing or intranet-facing application server, and you must harden hosts on the network against these vulnerabilities.
title: Network layer security
exl-id: 0a45d18a-66aa-4ecc-8eaf-e2af599eb3b8
---
# Network layer security{#network-layer-security}

Network security vulnerabilities are among the first threats to any Internet-facing or intranet-facing application server, and you must harden hosts on the network against these vulnerabilities.

Here are some common techniques that reduce network security vulnerabilities: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Technique </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Demilitarized zones (DMZs) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Segmentation must exist in at least two levels with the application server that is used to run Adobe Primetime DRM when Primetime DRM is behind the inner firewall. You must separate the external network from the DMZ that includes the web servers, and the web servers must be separated from the internal network. You can use firewalls to implement these layers of separation. </p> <p>You can categorize and control the traffic that passes through each network layer to ensure that only the absolute minimum of required data is allowed. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Private IP addresses </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use Network Address Translation (NAT) with RFC 1918 private IP addresses on Primetime DRM application servers. You can assign private IP addresses (10.0.0.0/8, 172.16.0.0/12 and 192.168.0.0/16) to make it more difficult for an attacker to route traffic to and from a NAT internal host through the Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Here are some criteria to consider when selecting a firewall solution: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implement firewalls that support proxy servers and/or stateful inspection, instead of simple packet-filtering solutions. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Use a firewall that supports a security paradigm in which you can deny all services, except the explicitly permitted services. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implement a firewall solution that is dual-homed or multi-homed. This architecture provides the greatest level of security and prevents unauthorized users from bypassing the firewall security. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
