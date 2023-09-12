---
description: When you configure a secure network architecture, network protocols are required for interaction between Adobe Primetime DRM and other systems in your enterprise network.
title: Adobe Primetime DRM network protocols
exl-id: d5720ef4-6845-4a62-940a-9d8ba9b43b13
---
# Adobe Primetime DRM network protocols {#adobe-primetime-drm-network-protocols}

When you configure a secure network architecture, network protocols are required for interaction between Adobe Primetime DRM and other systems in your enterprise network.

When you configure a secure network architecture, the following network protocols are required for this interaction: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocol </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR®, and Adobe Primetime clients communicate with Primetime DRM over HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (Optional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player, Adobe AIR, and Adobe Primetime clients can use HTTPS to communicate with Primetime DRM; HTTPS (SSL) is not required unless you support FMRMS 1.x clients. For more information, see <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> Incoming URLs </a> and Configuring SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Ports for application servers {#ports-for-application-servers}

You can configure the Adobe Primetime DRM license server to use any network port.

These ports must be enabled or disabled on the inner firewall, depending on the network functionality that you want to allow for clients that connect to the application server that runs Primetime DRM.

## Configuring SSL {#configuring-ssl}

The Secure Sockets Layer (SSL) is necessary only if you require support for Flash Media Rights Management Server 1.x clients.

SSL with client authentication is required for the Adobe Primetime DRM Key Server. For more information, see [Using the Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).
