---
title: DRM Revocation List Manager
description: DRM Revocation List Manager
copied-description: yes
exl-id: 5b17d195-30ca-4005-b710-83a6f77779a2
---
# DRM Revocation List Manager {#policy-revocation-list-manager}

Use the Primetime DRM Revocation List Manager command-line tool ( [!DNL AdobeRevocationListManager.jar]) to create and manage revocation lists, and to check whether policies have been revoked.

Before you run [!DNL AdobeRevocationListManager.jar], you must set properties in the *Policy Update List Manager and Revocation List Manager Properties* section of your configuration file. 

>[!NOTE]
>
>You can also specify all Revocation List Manager properties from the command line.

## Revocation List Manager command-line usage {#revocation-list-manager-command-line-usage}

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

* `destfile` specifies the name of the file in which the revocation list properties are saved. 
* `crlNumber` represents a non-negative version number of the Certificate Revocation List (CRL). You need to increment this number each time the CRL is updated.

**Table 5: Command-line Options**

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
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Specifies the name and location of the configuration file. </p><p class="- topic/p ">If you do not specify a name or a location, the DRM Revocation List Manager searches for <span class="filepath"> flashaccesstools.properties</span> in the current working directory. </p><p>Note:  Options that you specify on the command line take precedence over the options you specify in the configuration file. </p>Specifies the location of the configuration file. If you do not apply this option, the Revocation List Manager searches for <span class="filepath"> flashaccesstools.properties</span> in the working directory. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d filename</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Displays information about the revocation list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e date</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Optional) The expiration date of the revocation list. Use one of the following formats: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>For example, 2009-01-31-14:30:00 represents January 31 at 2:30 PM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Adds all entries from the existing revocation list. You can only specify one existing file. </p> <p class="- topic/p ">If the existing list was signed with a credential other than the one that you have used to sign the new list, you need to specify its certificate file next to verify its signature. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o</span> is not set, an error occurs. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> If the destination file already exists, you can overwrite it without being prompted. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revokes the certificate that has been identified by <span class="codeph"> issuerName</span> and <span class="codeph"> serialNumber</span> on the specified date. The <span class="codeph"> issuerName</span> must use the 509 name format. For example, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>You must specify the serial numbers in a hexadecimal format. You also need to specify the revocation date in one of the following formats: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>For example, 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. If you do not specify the revocation date, the current date is automatically applied. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Configuration properties {#configuration-properties}

You need to apply credentials to sign revocation lists. The following Revocation List Manager properties specify a PKCS12 file that includes credentials for signing revocation lists (License Server Certificate), along with the password for the cert:

* `revocation.sign.certfile=license-server-credentials.pfx` 
* `revocation.sign.certpass=password`
