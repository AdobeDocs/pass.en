---
title: Overview
description: Overview
copied-description: yes
exl-id: 866b3147-c28b-41b0-8653-06ba867354c5
---
# DRM Media Packager {#media-packager}

Use the Media Packager ( [!DNL AdobePackager.jar]) to specify a DRM policy to apply to your content, and to specify which part of the content to encrypt. For example, you can specify that the packager should encrypt the video data, but not the audio data.

Before you run [!DNL AdobePackager.jar], you must set properties in the Media Packager Properties section of your configuration file. 

>[!NOTE]
>
>You can also specify all Media Packager properties from the command line.

## Media Packager command-line usage {#media-packager-command-line-usage}

**Package one file:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` - The name of the file that you want to encrypt. 
* `dest` - The name of the resulting encrypted file.

  If you specify a directory, then the encrypted file is automatically saved in the specified directory with the same file name that you specified as the source file. However, you cannot specify a destination directory that includes the source file.

**Package multiple files with the same key** (for multi-bit-rate support):

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` - A series of whitespace-delimited source entries for the files that you want to encrypt. 
* `dest-directory` - The destination directory where you want to write encrypted content. The encrypted files are automatically saved in this directory using the same file names as the source files. However, the destination directory cannot include any source files.

**View information about an encrypted file:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**View information about a metadata file:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` is a [!DNL .metadata] file that includes DRM metadata.

>[!NOTE]
>
>During packaging, the Media Packager can no longer generate a [!DNL .header] file by default. To generate a [!DNL .header] file, use the `-h` option during packaging.

**Table 3: Options**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Command line option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the name and location of the configuration file. </p> <p class="- topic/p ">If you do not specify a name or a location, the DRM Media Packager searches for <span class="filepath"> flashaccesstools.properties </span> in the current working directory. </p> <p>Note:  Options that you specify on the command line take precedence over the options you specify in the configuration file. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Enables you to view information about a file that has already been packaged. </p> <p class="- topic/p ">The source and destination files are not required. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Enables you to view information about existing metadata. </p> <p class="- topic/p ">The source and destination files are not required. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extracts DRM policies from a packaged file when you apply this option in conjunction with the <span class="codeph"> -d </span> option. </p> <p class="- topic/p ">A file is automatically created in the same directory in which the encrypted file is located with a file name and DRM policy identifier. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extracts the DRM header from a packaged file when you apply this option in conjunction with the <span class="codeph"> -d </span> option. </p> <p class="- topic/p ">A file is automatically created in the same directory in which the encrypted file, is located with the file name and the extension <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies a unique identifier for this segment of content. </p> <p class="- topic/p ">If you do not specify an identifier, then the destfile file name is automatically applied. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> value </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies a custom key/value to add to content metadata. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -k </span> options. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extract metadata from a packaged file when you apply this option in conjunction with the <span class="codeph"> -d </span> option. </p> <p class="- topic/p ">A file is automatically created in the same directory as the encrypted file with a file name and a <span class="codeph"> .metadata </span> extension. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask whether the destination file should be overwritten. </p> <p class="- topic/p ">If the destination file already exists and <span class="codeph"> -o </span> is not set, then an error occurs. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Overwrites the destination file without you being prompted unless it already exists. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> filename [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the name of the file that includes the DRM policy. </p> <p class="- topic/p ">If the DRM policy requires domain registration with a server that uses a transport certificate other than the one that you have specified in the properties file, then you need to provide the domain transport certificate. </p> <p class="- topic/p ">You can specify multiple <span class="codeph"> -p </span> options. The client always applies the first option by default. The values that you have specified on the command line takes precedence over those that you have specified in the configuration file. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Configuration properties {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>For property names that include* n*, *n* represents an integer that starts with 1 and increases for each instance of the property.

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
   <td colname="2" class="- topic/entry "> <p>Indicates whether to encrypt script data in mp4s. </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> and <i class="+ topic/ph hi-d/i ">onXMP</i> script data tags are never encrypted even if you enable this option. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indicates the video encryption level. </p> <p class="- topic/p ">A value of <span class="codeph"> high</span> is used to encrypt all video content, while values of <span class="codeph"> medium</span> and <span class="codeph"> low</span> are used to encrypt portions of the video content for mp4 files that include H.264 content. </p> <p class="- topic/p ">value = <span class="codeph"> high | medium | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If a value is greater than 0, then the specified number of seconds of content at the beginning of the file are not encrypted. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license server certificate file used to encrypt the key. </p> <p class="- topic/p ">The <span class="codeph"> encrypt.keys.asymmetric.certfile</span> property specifies a file that includes the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">This property is used repeatedly to create a list of DRM policies to apply to the content. <span class="codeph"> n</span> represents an integer whose value is 1 or greater. The client uses the first instance by default. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The license server URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The transport certificate for the license server. </p> <p class="- topic/p ">This property specifies a <span class="filepath"> .cer</span> file that includes the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The PKCS12 file that includes packager credentials for signing content. </p> <p class="- topic/p ">The <span class="codeph"> encrypt.sign.certfile</span> needs to refer to a <span class="filepath"> .pfx</span> file that includes a certificate and private key. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">The password that you can apply to protect the file which has been specified by <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sets the minimum server version that is required to issue licenses for the content being packaged. </p> <p class="- topic/p ">Specify x (for Primetime DRM x.0) where x represents a major release number. Any versions of servers that precede Adobe Primetime version 3.0 do not support this setting. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If a DRM policy <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requires domain registration with a server that supports a transport certificate other than the one that you have specified in <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, then you need to provide the domain transport certificate needs. </p> <p class="- topic/p ">This property specifies a file that includes the certificate only (either PEM or DER format is acceptable). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies a license key. </p> <p class="- topic/p ">If you do not specify a key, then the key is randomly generated. When you do not enable key rotation, then you can use this key to encrypt content. </p> <p class="- topic/p ">When you enable key rotation, you can use this key to protect the rotation keys. The key must be 16 bytes in length and be specified as Hex values. Whitespace between the Hex values is optional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies whether key rotation is enabled. </p> <p class="- topic/p ">If set to false, which is the default setting, then key rotation is disabled and the master CEK is used to encrypt all samples in the content. </p> <p class="- topic/p ">If set to true, key rotation is enabled and different keys can be used to encrypt segments of any content. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sequence of rotated keys that you can specify to encrypt content when key rotation is enabled. </p> <p class="- topic/p ">If you do not specify any keys, then keys are randomly generated. The keys must be 16 bytes in length and specified as Hex values. </p> <p class="- topic/p ">Whitespace between the Hex values is optional. <i class="+ topic/ph hi-d/i ">n</i> must be monotonically increasing, starting from 1. When you specify multiple keys, then keys are cycled through in the order that you indicated. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the interval of time in seconds during which you can apply a rotation key to encrypt content samples. </p> <p class="- topic/p ">After the interval of time has elapsed in which the content has been encrypted, then the next rotation key is then applied. If you have enabled key rotation but have not specified any interval of time, then the keys are automatically rotated every 15 minutes. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">If this option is set to true, then a license server from which licenses can be obtained is not available. </p> <p class="- topic/p ">Licenses must be embedded or obtained out-of-band. The default value is set to false unless you specify a different value. This option is only supported in Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
