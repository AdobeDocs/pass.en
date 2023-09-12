---
title: Network layer security
description: Network layer security
copied-description: yes
exl-id: 70c9917d-32bc-43f6-add3-62883f98ac5e
---
# Network layer security{#network-layer-security}

Network security vulnerabilities are among the first threats to any Internet-facing or intranet-facing application server. This section describes the process of hardening hosts on the network against these vulnerabilities. It addresses network segmentation, Transmission Control Protocol/Internet Protocol (TCP/IP) stack hardening, and the use of firewalls for host protection.

This table describes common techniques that reduce network security vulnerabilities. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Technique </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Demilitarized zones (DMZs) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Segmentation must exist in at least two levels with the application server used to run Adobe Access placed behind the inner firewall. Separate the external network from the DMZ that contains the web servers, which in turn must be separated from the internal network. Use firewalls to implement the layers of separation. Categorize and control the traffic that passes through each network layer to ensure that only the absolute minimum of required data is allowed. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Private IP addresses </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use Network Address Translation (NAT) with RFC 1918 private IP addresses on Adobe Access application servers. Assign private IP addresses (10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16) to make it more difficult for an attacker to route traffic to and from a NAT internal host through the Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use the following criteria to select a firewall solution: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implement firewalls that support proxy servers and/or stateful inspection instead of simple packet-filtering solutions. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Use a firewall that supports a security paradigm in which you can deny all services except those explicitly permitted. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implement a firewall solution that is dual-homed or multi-homed. This architecture provides the greatest level of security and helps to prevent unauthorized users from bypassing the firewall security. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
