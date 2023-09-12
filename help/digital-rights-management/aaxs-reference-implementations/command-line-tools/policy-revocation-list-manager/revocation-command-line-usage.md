---
title: Command line usage
description: Command line usage
copied-description: yes
exl-id: b9e51bab-7bef-459f-bb4d-13ccc4add37a
---
# Command line usage {#command-line-usage}

Revocation List Manager is in the \Reference Implementation\Command Line Tools directory on the DVD. To run the tool, use one of the following syntaxes:

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` indicates where the revocation list will be written. 
* `crlNumber` is a non-negative version number of the Certificate Revocation List (CRL). This number should be incremented each time the CRL is updated.

The following table contains descriptions of the command line options shown in the syntax above: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Command line option </th> 
   <th colname="2" class="- topic/entry entry"> Description </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c configfile</span> </td> 
   <td colname="2" class="- topic/entry ">Specifies the location of the configuration file. If this option is not used, the Revocation List Manager will look for <span class="filepath"> flashaccesstools.properties</span> in the working directory. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d filename</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Displays information about the revocation list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e date</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Optional) The expiration date of the revocation list. Use the format <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> or <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> (for example, 2009-01-31-14:30:00 represents January 31 at 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Adds all entries from the existing revocation list. Only one existing file may be specified. <p class="- topic/p ">If this existing list was signed with a different credential than the one being used to sign the new list, specify its certificate file next, so its signature can be verified. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file already exists and -o is not set, an error will be returned. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> If the destination file already exists, overwrite it without prompting. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revokes the certificate identified by <span class="codeph"> issuerName</span> and <span class="codeph"> serialNumber</span> on the given date. The <span class="codeph"> issuerName</span> must follow the 509 name format (for example, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Specify serial numbers in hexadecimal form. Specify the revocation date as <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> or <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>, for example 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. If the revocation date is not specified, the current date is used. </p> </td> 
  </tr> 
 </tbody> 
</table>
