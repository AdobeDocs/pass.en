---
title: Command line usage
description: Command line usage
copied-description: yes
exl-id: 4c772010-b7b6-4655-98ee-b52e8022d4af
---
# Command line usage {#command-line-usage}

Policy Update List Manager is in the \Reference Implementation\Command Line Tools directory on the DVD. To create a policy update list, use the following syntax:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indicates where the policy update list will be written.

To view an existing policy update list, use the following syntax: 

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

The following table contains descriptions of the command line options shown in the syntax above: 

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the location of the configuration file. If this option is not used, the Policy Update List Manager will look for <span class="filepath"> flashaccesstools.properties </span> in the working directory. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d filename </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Displays information about the policy update list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e date </span> </td> 
   <td colname="2" class="- topic/entry "> (Optional) The expiration date of the policy update list. Use the format <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> (for example, 2009-01-31-14:30:00 represents January 31 at 2:30 PM). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f filename [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adds all entries from the existing policy update list. Only one existing file may be specified. </p> <p class="- topic/p ">If this existing list was signed with a different credential than the one being used to sign the new list, specify its certificate file, so its signature can be verified. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o </span> is not set, an error will be returned. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If the destination file already exists, overwrite it without prompting. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Optional) Revokes the policy ID on the specified date. An optional reason code, reason text, and reason URL may also be provided. Specify an empty string "" to indicate that no value is provided for the optional parameters. Specify the date as <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> (for example 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008). If a date is not specified, the current date is used. The reason code must be greater than or equal to 0. Multiple -r options may be specified. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Performs the same action as the -r flag, but extracts the policy identifier from the given file. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Replaces any matching policy in a license request with this policy using the given reason code (optional), reason text (optional), and reason URL (optional). </p> <p>Specify an empty string "" to indicate that no value is provided for the optional parameters. </p> <p>The reason code must be greater than or equal to <span class="codeph"> 0 </span>. Multiple <span class="codeph"> -u </span> options may be specified. </p> </td> 
  </tr> 
 </tbody> 
</table>
