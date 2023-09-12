---
title: Command line usage
description: Command line usage
copied-description: yes
exl-id: 2142cb76-e71c-4443-8b5d-348e45587331
---
# Command line usage {#command-line-usage}

Before using Policy Manager, ensure that you fulfill the requirements listed in Requirements.

Policy Manager is in the [!DNL \Reference Implementation\Command Line Tools] directory on the DVD. To run the tool, use the following syntax:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

The following table contains descriptions of the command line actions shown in the syntax above: 

|  Command line action  | Description  |
|---|---|
|  `new`  | Creates a new policy.  |
|  `detail`  | Describes an existing policy.  |
|  `update`  | Updates an existing policy.  |

The following table describes the command line options that can be specified along with the syntax above: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Command line option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the location of the configuration file. If this option is not used, the Policy Manager will look for <span class="filepath"> flashaccesstools.properties </span> in the working directory. Options specified on the command line take precedence over those present in the configuration file. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If the destination file already exists, overwrite it without prompting. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o </span> is not set, an error will be returned. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates the policy has a root license. Not allowed for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The date before which licenses will be valid. Specify as <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. For example, 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. The value must be greater than the value of <span class="codeph"> -s </span>, if present. This option cannot be used with <span class="codeph"> -r </span>. To remove the end date when updating a policy, use <span class="codeph"> -e </span> without specifying a date. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutes </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The duration (minutes) that content protected with this policy is valid, beginning when the content is protected with the packager. The value must be non-negative. This option cannot be used with <span class="codeph"> -e </span>. To remove the duration when updating a policy, use <span class="codeph"> -r </span> without specifying a number of minutes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The date after which licenses will be valid. Specify as <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. For example, 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. The value must be less than the value of <span class="codeph"> -e </span>, if present. This option cannot be used with <span class="codeph"> -r </span>. To remove the start date when updating a policy, use <span class="codeph"> -s </span> without specifying a date. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minutes </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The playback window (the number of minutes the content may be viewed, beginning from the first playback). If this option is not specified or if <span class="codeph"> -w </span> is used without specifying the number of minutes, there is no playback window limitation. The value must be non-negative. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutes </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license caching duration in minutes, which is the time a license will be allowed to be cached in the client's License Store after the license has been issued by the server. The value must be non-negative. Specify <span class="codeph"> -l 0 </span> to indicate license caching is not permitted. Use <span class="codeph"> -l </span> without specifying a number of minutes for unlimited license caching. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license caching end date (the date after which licenses may not be cached in the client's License Store, after the license has been issued by the server). Specify as <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span><i class="+ topic/ph hi-d/i "> </i>or<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>. For example, 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. Use <span class="codeph"> -l </span> without specifying a number of minutes for unlimited license caching. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The authentication namespace. If specified, the client should authenticate with a user name and password issued by the specified authority. This option cannot be used with <span class="codeph"> -x </span>. It is not allowed for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Allow anonymous access. This option cannot be used with <span class="codeph"> -authNS </span>. It is not allowed for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">An allow list of AIR applications allowed to play protected content. Use this to restrict which publishers, applications, and versions may access content protected with this policy. </p> <p class="- topic/p ">If <i class="+ topic/ph hi-d/i ">appId</i> is not specified, all applications for publisher <i class="+ topic/ph hi-d/i ">pubId</i> are allowed. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min</i> and <i class="+ topic/ph hi-d/i ">max</i> version numbers are optional. </p> <p class="- topic/p ">Multiple <span class="codeph"> -air </span> options may be specified to allow multiple applications. If no AIR or SWF applications are specified, all applications may access this content. During an update, use -air without the remaining arguments to remove all entries from the list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The DRM clients restricted from accessing protected content. The value consists of comma separated name:value pairs with the following format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">For example, <span class="codeph"> os=Win,release=2.0.1 </span>. During an update, use <span class="codeph"> -drmBlacklist </span> without the remaining arguments to remove all entries from the list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates that DRM clients must have the specified minimum security level to access protected content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | REQUIRED | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Analog output protection constraints. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | REQUIRED | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Digital output protection constraints. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The application runtimes restricted from accessing protected content. The value consists of comma separated name:value pairs with the following format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | application | release= stringValue </span> </p> <p class="- topic/p ">For example, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. During an update, use <span class="codeph"> -runtimeBlacklist </span> without the remaining arguments to remove all entries from the list. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates that the application runtimes must have the specified minimum security level to access protected content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">An allow list of SWF applications allowed to play protected content. Multiple -swf options may be specified to allow multiple applications. If no AIR or SWF applications are specified, all applications may access this content. During an update, use -swf without the remaining arguments to remove all entries from the list. To identify a SWF by its hash value, specify the SWF file for which to compute the hash and the maximum time to allow for SWF verification to complete (in seconds). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies custom key/values to add to the policy. Multiple <span class="codeph"> -k </span> options may be specified. During update, use <span class="codeph"> -k </span> without the remaining arguments to remove all properties. The interpretation or handling of this data is completely up to the implementation of the Adobe Access license server. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adds a custom property, which will appear in the license generated for each client. Multiple <span class="codeph"> -p </span> options may be specified to add multiple properties. During an update, use <span class="codeph"> -p </span> without the remaining arguments to remove all properties. The interpretation or handling of this data is completely up to the implementation of the client application. </p> </td> 
  </tr> 
 </tbody> 
</table>
