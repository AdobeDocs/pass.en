---
title: Vendor-specific security information
description: Vendor-specific security information
copied-description: yes
exl-id: 668321c5-b2c7-4bb3-9f68-2dba622a54de
---
# Vendor-specific security information{#vendor-specific-security-information}

This section contains security-related information about operating systems and application servers that are incorporated into your Adobe Access solution.

Use the links provided in this section to find vendor-specific security information for your operating system and application server.

## Operating system security information {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

When securing your operating system, carefully implement the measures that are described by your operating system vendor, including these:

* Defining and controlling users, roles, and privileges 
* Monitoring logs and audit trails 
* Removing unnecessary services and applications 
* Backing up files

For security information about operating systems that Adobe Access supports, see the resources in this table. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

The following table describes some potential approaches to minimizing security vulnerabilities that are found in the operating system. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Item </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Security patches </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">There is an increased risk that an unauthorized user may gain access to the application server if vendor security patches and upgrades are not applied in a timely fashion. Test security patches before you apply them to production servers. </p> <p class="- topic/p ">Also, create policies and procedures to check for and install patches on a regular basis. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Virus protection software </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Virus scanners can identify infected files by scanning for a signature or watching for unusual behavior. Scanners keep their virus signatures in a file, which is usually stored on the local hard drive. Because new viruses are discovered often, you must frequently update this file in order for the virus scanner to identify all current viruses. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">For both proper operation and forensic analysis, keep accurate time on Adobe Access servers and Adobe Access packagers. Use a secure version of NTP to synchronize the time on all systems that are connected to the Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Application server security information {#section-EBB4EF371CFF4A848694CC240B23D404}

When securing your application server, you must implement the measures that are described by your server vendor, including these:

* Using non-obvious administrator user name 
* Disabling unnecessary services 
* Securing the console manager 
* Enabling secure cookies 
* Closing unneeded ports 
* Limiting administrative interfaces by IP addresses or domains 
* Using the Java™ Security Manager
