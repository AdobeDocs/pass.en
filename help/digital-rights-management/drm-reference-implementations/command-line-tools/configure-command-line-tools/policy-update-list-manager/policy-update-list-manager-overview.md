---
title: Overview
description: Overview
copied-description: yes
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
---
# DRM Policy Update List Manager {#policy-update-list-manager}

Use the Primetime DRM Policy Update List Manager command-line tool ( [!DNL AdobePolicyUpdateListManager.jar]) to create and manage DRM policy update lists, and to check whether policies have been updated or revoked.

Before you run the Policy Update List Manager command-line tool, you must set properties in the *Policy Update List Manager and Revocation List Manager Properties* section of your configuration file. 

>[!NOTE]
>
>You can also specify all Policy Update List Manager properties from the command line.

## Policy Update List Manager command-line usage {#policy-update-list-manager-command-line-usage}

**Create a policy update list:** 

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indicates the name of the file into which the DRM policy update list is written.

**View an existing policy update list:** 

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` The name of the policy update list file.

**Table 4: Command-line options**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Command line option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the name and location of the configuration file. </p> <p class="- topic/p ">If you do not specify a name or a location, the DRM Policy Update List Manager searches for <span class="filepath"> flashaccesstools.properties </span> in the current working directory. </p> <p>Note:  Options that you specify on the command line take precedence over the options you specify in the configuration file. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d filename </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Displays information about the DRM policy update list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e date </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Optional) The expiration date of the DRM policy update list. </p> <p>Use the format <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> (for example, 2009-01-31-14:30:00 represents January 31 at 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filename [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adds all entries from the existing DRM policy update list. You can only specify one existing file. </p> <p class="- topic/p ">If the existing list has been signed with a credential other than the one being used to sign the new list, then you need to specify its certificate file to verify its signature. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o </span> is not set, an error occurs. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If the destination file already exists, overwrite it without prompting. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Optional) Revokes the DRM policy ID on the specified date. You can provide an optional reason code, reason text, and reason URL. You need to specify an empty string "" to indicate that no value is provided for the optional parameters. You can specify the date in <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> in these formats. For example, 2008-12-1 or 2008-12-1-00:00:00 represents midnight on December 1, 2008). If you do not specify a date, then the current date is automatically applied. Therefore the reason code must be greater than or equal to 0. You can also specify multiple -r options. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Performs the same action as the <span class="codeph"> -r </span> option. However, it extracts the DRM policy identifier from a specified file. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Replaces any matching DRM policy in a license request with this DRM policy by using the given reason code (optional), reason text (optional), and reason URL (optional). </p> <p>An empty string "" indicates that you have not provided any value for the optional parameters. </p> <p>The reason code must be greater than or equal to <span class="codeph"> 0 </span>. You can specify multiple <span class="codeph"> -u </span> options. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Configuration properties {#configuration-properties}

The following Primetime DRM Policy Update List Manager properties specify a PKCS12 file that includes credentials for signing revocation lists (License Server Certificate), along with a password.

* `revocation.sign.certfile=license-server-credentials.pfx` 
* `revocation.sign.certpass=password`
