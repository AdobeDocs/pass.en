---
title: Policy Manager Command-line usage
description: Policy Manager Command-line usage
copied-description: yes
exl-id: 888be282-7eaa-4101-b4b1-4f8df99a967a
---
# Policy Manager Command-line usage {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Table 1: Commands**

|  Command  | Description  |
|---|---|
|  `new`  | Creates a new DRM policy  |
|  `detail`  | Describes an existing DRM policy  |
|  `update`  | Updates an existing DRM policy  |

**Table 2: Options**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Command-line option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c configfile </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the name and location of the configuration file. </p> <p class="- topic/p ">If you do not specify a name or a location, the DRM Policy Manager searches for <span class="filepath"> flashaccesstools.properties </span> in the current working directory. </p> <p>Note:  Options that you specify on the command line take precedence over the options you specify in the configuration file. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If the destination file exists, you can overwrite the file without being prompted. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask if the destination file should be overwritten. If the destination file exists and <span class="codeph"> -o </span> is not set, an error occurs. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates that the DRM policy has a root license. </p> <p class="- topic/p ">This option is not available for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The date before licenses becomes valid. </p> <p>You can specify the date in <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> format. For example, 2008-12-1 or 2008-12-1-00:00:00 for midnight on December 1, 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">The value must be greater than the value of <span class="codeph"> -s </span> if present. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">You cannot apply this option with <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">To remove the end date when you update a DRM policy, apply <span class="codeph"> -e </span> without specifying a date. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minutes </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The duration in minutes that the protected content is valid. </p> <p class="- topic/p ">The DRM policy becomes valid when the content is protected with the packager. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">The value must be non-negative. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">You cannot apply this option along with <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">To remove or delete the duration when you update a DRM policy, apply <span class="codeph"> -r </span> without specifying any minutes. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The date that the licenses become valid. </p> <p>You can specify the date in the <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> or <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> format. For example, <span class="codeph"> 2008-12-1 </span> or <span class="codeph"> 2008-12-1-00:00:00 </span> for midnight on December 1, 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">The value must be less than the value of <span class="codeph"> -e </span>, if present. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">You cannot apply this option along with <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">To remove or delete the start date when you update a DRM policy, use <span class="codeph"> -s </span> without specifying a date. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Playback window, which is the number of minutes the content can be viewed from the first playback. </p> <p>If unspecified, or if <span class="codeph"> -w </span> is used without specifying a number of minutes, there is no playback window limitation. The value must be non-negative. </p> <p>The optional <span class="codeph"> enableHS </span> or <span class="codeph"> disableHS </span> flag signals whether to enable or disable hard stop. The flag indicates whether the decryption context is destroyed at the end of the playback window (enabled) or not destroyed (disabled). </p> <p>For example, to specify that the content may only be viewed for 60 minutes and requires hard stop: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>Note:  <i>Hard stop</i> is not currently supported in Flash Player, Android, and iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minutes </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license caching duration is the time in minutes that a license can be cached in the client's License Store after the license has been issued by the server. The value must be non-negative. </p> <p>You can specify <span class="codeph"> -l 0 </span> to indicate that license caching is not permitted. For unlimited license caching, specify <span class="codeph"> -l </span> without any minutes. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -ldate date </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license caching end date. </p> <p class="- topic/p ">This indicates the final date that the client can cache licenses in the client's License Store after the Primetime DRM server has issued the license. </p> <p>You can specify the date in the following formats: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> </li> 
     </ul>For example, <span class="codeph"> 2008-12-1 </span> or <span class="codeph"> 2008-12-1-00:00:00 </span> for midnight on December 1, 2008. You need to apply <span class="codeph"> -l </span> without specifying any minutes for unlimited license caching. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The authentication namespace. </p> <p class="- topic/p ">If you apply this option, then the client needs to enter a user name and password that was issued by the specified authority. </p> <p>You cannot apply this option along with <span class="codeph"> -x </span>. </p> <p>This option is not allowed for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Allow anonymous access. </p> <p class="- topic/p ">You cannot apply this option along with <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">This option is not allowed for updates. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A allow list of AIR applications that can play protected content. </p> <p class="- topic/p ">You can apply this option to restrict which publishers, applications, and versions can access the content that is protected with this DRM policy. </p> <p class="- topic/p ">If you do not specify <i class="+ topic/ph hi-d/i ">appId</i>, all of the applications for publisher <i class="+ topic/ph hi-d/i ">pubId</i> are allowed. </p> <p>Note:  <i class="+ topic/ph hi-d/i ">min</i> and <i class="+ topic/ph hi-d/i ">max</i> version numbers are optional. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -air </span> options to allow multiple applications. If you do not specify an AIR or SWF application, all of the applications can access this content. During an update, to remove or delete all entries from the list, apply <span class="codeph"> -air </span> without the remaining arguments . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The DRM clients that are restricted from getting access to protected content. </p> <p class="- topic/p ">The value supports comma-separated name:value pairs in the following format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue </span> </p> <p class="- topic/p ">For example, <span class="codeph"> os=Win,release=2.0.1 </span>. During an update, to remove all entries from the list, apply <span class="codeph"> -drmBlacklist </span> without the remaining arguments. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates that DRM clients must have an assigned minimum security level to get access to protected content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | REQUIRED | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Analog output protection constraints </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | REQUIRED | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Digital output protection constraints </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist name </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> value </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> pairs </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The application runtimes that are restricted from accessing protected content. </p> <p class="- topic/p ">The value support comma-separated name:value pairs in the following format: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | application | release= stringValue </span> </p> <p class="- topic/p ">For example, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. During an update, to remove all entries from the list, apply <span class="codeph"> -runtimeBlacklist </span> without the remaining arguments . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates that the application runtimes must have a specified minimum security level to access protected content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf url </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A allow list of SWF applications that are allowed to play protected content. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -swf </span> options to allow multiple applications. If you do not specify any AIR or SWF applications, all of the applications can access this content. </p> <p>During an update, to remove all entries from the list, apply <span class="codeph"> -swf </span> without the remaining arguments . If you want to identify a SWF by its hash value, you need to specify the SWF file for which to compute the hash and the maximum time to allow for SWF verification to complete (in seconds). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies custom key/values that you want to add to a DRM policy. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -k </span> options. During update, you can apply <span class="codeph"> -k </span> without the remaining arguments if you want to remove all properties. The interpretation or handling of the data is managed by the Primetime DRM license server. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Adds a custom property that appears in the license generated for each client. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -p </span> options to add multiple properties. During an update, you need to apply <span class="codeph"> -p </span> without the remaining arguments if you want to remove all properties. The interpretation or handling of this data is managed by the implementation of the client application. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> Over the air (OTA) output protection constraints. The <span class="codeph"> whitelist </span> field specifies which connection types to allow list and the format of &lt;connection types&gt; is <span class="codeph"> [type(,type)*] </span>, where type can be any of the following: MIRACAST, AIRPLAY, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Resolution-based output protection constraints as defined in the specified file. </p> <p>The encoding of this file is JSON. The grammar for the formatting can be found in <i>About Resolution-Based Output Protection</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Examples**

To create a policy that allows anonymous access to your content, using your own configuration properties file: 

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
