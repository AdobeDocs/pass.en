---
title: Configuration file properties
description: Configuration file properties
copied-description: yes
exl-id: eec6a53d-d831-4ec4-a90c-8b3e7997f330
---
# Configuration file properties {#configuration-file-properties}

Before you run Media Packager, specify values for the Media Packager properties. The configuration file specifies the following properties. For property names that include* n*, *n* represents an integer starting with 1 and increasing for each instance of the property. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Property </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indicates whether to encrypt video content. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indicates whether to encrypt audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">Indicates whether to encrypt script data in FLVs. <i class="+ topic/ph hi-d/i ">onMetaData</i> and <i class="+ topic/ph hi-d/i ">onXMP</i> script data tags are never encrypted, even if this option is enabled. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates the video encryption level. A value of high is used to encrypt all video content, while values of medium and low are used to encrypt portions of the video content for F4V files containing H.264 content. </p> <p class="- topic/p ">value = <span class="codeph"> high | medium | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If the value is greater than 0, the specified number of seconds of content at the beginning of the file will not be encrypted. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license server certificate file used to encrypt the key. The <span class="codeph"> encrypt.keys.asymmetric.certfile</span> property specifies a file that contains the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">This property is used repeatedly to create a list of policies to apply to the content. <span class="codeph"> n</span> is an integer whose value is 1 or greater. The client will use the first instance by default. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license server URL. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The transport certificate for the license server. This property specifies a <span class="filepath"> .cer</span> file that contains the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The PKCS12 file containing packager credentials for signing content. The <span class="codeph"> encrypt.sign.certfile</span> should refer to a <span class="filepath"> .pfx</span> file containing a certificate and private key. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The password used to protect the file specified by <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sets the minimum server version required to issue licenses for the content being packaged. Specify x (Adobe Access x.0) where x = the major release number. Servers before Adobe Access 3.0 do not support this setting. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If a policy <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requires domain registration with a server that uses a different transport certificate than specified in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, the domain transport certificate needs to be provided. </p> <p class="- topic/p ">This property specifies a file that contains the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specify license key. If no key is specified, the key will be randomly generated. When key rotation is not enabled, this is the key used to encrypt the content. </p> <p class="- topic/p ">When key rotation is enabled, this key is used to protect the rotation keys. The key must be 16 bytes in length and specified as Hex values. Whitespace between the Hex values is optional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies whether key rotation is enabled. If set to false (default), key rotation is disabled and the master CEK will be used to encrypt all samples in the content. </p> <p class="- topic/p ">If set to true, key rotation will be enabled, and different keys can be used to encrypt portions of the content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequence of rotated keys used to encrypt content when key rotation is enabled. If no keys are specified, keys will be randomly generated. The keys must be 16 bytes in length and specified as Hex values. </p> <p class="- topic/p ">Whitespace between the Hex values is optional. <i class="+ topic/ph hi-d/i ">n</i> must be monotonically increasing, starting from 1. When multiple keys are specified, the keys will be cycled through in the order indicated. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the interval (in seconds) during which a rotation key will be used to encrypt content samples. </p> <p class="- topic/p ">After this amount of time in the content has been encrypted, the next rotation key will be used. If key rotation is enabled and no interval is specified, keys will be rotated every 15 minutes. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If true, there is no license server from which the licenses can be obtained. Licenses must be embedded or obtained out-of-band. Default is false if not specified. Only supported in Adobe Access Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
