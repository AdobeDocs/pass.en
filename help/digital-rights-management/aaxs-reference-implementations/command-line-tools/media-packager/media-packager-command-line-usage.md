---
title: Command line usage
description: Command line usage
copied-description: yes
exl-id: 55b18fee-b7d8-4a5a-91a7-a08cd23e7866
---
# Command line usage {#command-line-usage}

Before using Media Packager, ensure that you fulfill the requirements listed in Requirements and that the configuration file contains the required information (see Configuration file in the *Using the Adobe Access Reference Implementations*.

Media Packager is in the [!DNL \Reference Implementation\Command Line tools] directory on the DVD. To encrypt a single file, use the following syntax:

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

* `source` is the file to be encrypted. 
* `dest` specifies where the encrypted content will be written. If a directory is specified, the encrypted file will be saved in this folder using the same file name as the source file, but the directory must not be the directory which contains the source file.

To encrypt multiple files with the same key (for multi-bit-rate support), use the following syntax:

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

* `sourcefiles` is a series of whitespace-delimited source entries representing the files to be encrypted. 
* `dest-directory` specifies where the encrypted content will be written. The encrypted files will be saved in this folder using the same file names as the source files, but the directory must not be the directory that contains the source files.

To view information about an encrypted file, use the following syntax:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` is the encrypted file.

To view information about a metadata file, use the following syntax: 

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` is a [!DNL .metadata] file containing the DRM metadata.

>[!NOTE]
>
>During packaging, the Media Packager will no longer generate a .header file by default. To generate this file, use the `-h` option during packaging.

The following table contains descriptions of the command line options shown in the syntax above: 

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the location of the configuration file. If this option is not used the Media Packager will look for <span class="filepath"> flashaccesstools.properties </span> in the working directory. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Shows information about a file that was already packaged. The source and destination files are not required. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Shows information about existing metadata. The source and destination files are not required. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use this option with <span class="codeph"> -d </span> to extract policies from a packaged file. A file will be created in the same directory as the encrypted file using the file name and policy identifier. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use with <span class="codeph"> -d </span> to extract the DRM header from a packaged file. A file is created in the same directory as the encrypted file, using the file name and the extension <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies a unique identifier for this piece of content. If no identifier is specified, the destfile file name will be used. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> value </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies a custom key/value to add to content metadata. Multiple <span class="codeph"> -k </span> options may be specified. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use this option with <span class="codeph"> -d </span> to extract metadata from a packaged file. A file will be created in the same directory as the encrypted file using the file name and the extension <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Do not ask whether the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o </span> is not set, an error will be returned. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Overwrites the destination file without prompting, if it already exists. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> filename [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifies the name of the file containing the policy. If the policy requires domain registration with a server that uses a different transport certificate than the one specified in the properties file, the domain transport certificate also needs to be provided. </p> <p class="- topic/p ">Multiple <span class="codeph"> -p </span> options may be specified, and the client will use the first by default. The values specified on the command line take precedence over those specified in the configuration file. </p> </td> 
  </tr> 
 </tbody> 
</table>
