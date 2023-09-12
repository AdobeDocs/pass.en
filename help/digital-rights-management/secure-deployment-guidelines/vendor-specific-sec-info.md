---
description: Operating systems and application servers are included in your Adobe Primetime DRM solution.
title: Vendor-specific security information
exl-id: 4cc39414-cab5-4282-825d-64651d9b03e1
---
# Vendor-specific security information{#vendor-specific-security-information}

Operating systems and application servers are included in your Adobe Primetime DRM solution.

To find vendor-specific security information for your operating system and application server, see Using the Adobe Primetime DRM Key Server.

## Operating system security information {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

When securing your operating system, you must implement the measures that are described by your operating system vendor.

Here are some of the measures:

* Defining and controlling users, roles, and privileges 
* Monitoring logs and audit trails 
* Removing unnecessary services and applications 
* Backing up files

Here is some information about the operating systems that are supported by Adobe Primetime DRM: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Operating System </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Security Resource </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise or Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008 Security Guide</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5, and 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5 Security Guide</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

Here is some information about approaches to minimize security vulnerabilities in the operating system: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Item </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Security patches </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">There is an increased risk that an unauthorized user might gain access to the application server if vendor security patches and upgrades are not applied in a timely fashion. </p> <p>Note:  Ensure that you test security patches before applying them to production servers. </p> <p class="- topic/p ">You must create policies and procedures to regularly check for and install patches. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Virus protection software </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Virus scanners can identify infected files by scanning for a signature or unusual behavior. </p> <p>Scanners keep their virus signatures in a file, which is usually stored on the local hard drive. New viruses are discovered often, so you must ensure that this file is regularly updated. This way, virus scanners can always identify all current viruses. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">For proper operation and forensic analysis, keep accurate time on Primetime DRM servers and packagers. Use a secure version of NTP to synchronize the Primetime DRM time on all systems that are connected to the Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Application server security information {#section_22986936F1A547CEAB2D97E9E9D4825C}

When securing your application server, you must implement the measures that are described by your server vendor.

Here are some of these measures:

* Using non-obvious administrator user name 
* Disabling unnecessary services 
* Securing the console manager 
* Enabling secure cookies 
* Closing unneeded ports 
* Limiting administrative interfaces by IP addresses or domains 
* Using the Java™ Security Manager
