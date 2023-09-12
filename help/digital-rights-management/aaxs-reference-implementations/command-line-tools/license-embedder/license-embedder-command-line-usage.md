---
title: Command line usage
description: Command line usage
copied-description: yes
exl-id: 51b11ef8-438e-4747-be3e-e1774dc9f31a
---
# Command line usage {#command-line-usage}

To embed a license, use the following syntax:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` is an encrypted FLV or F4V file. 
* `destfile` specifies where the encrypted content with the embedded license will be written. If a directory is specified, the file will be saved in this directory using the same filename as the source file, but the directory must not be the directory which contains the source file.

The following table describes the command line options that can be specified along with the syntax previously mentioned: 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Command Line Option </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Description </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Name of the file containing license to embed. Multiple <span class="codeph"> -l </span> options may be specified to embed multiple licenses. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Specify the content metadata for which to generate a license. (Required to generate license) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> Do not ask if the destination file should be overwritten. If the destination file already exists and <span class="codeph"> -o </span> is not set, an error will be returned. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> If the destination file already exists, overwrite it without prompting. </td> 
  </tr> 
 </tbody> 
</table>
