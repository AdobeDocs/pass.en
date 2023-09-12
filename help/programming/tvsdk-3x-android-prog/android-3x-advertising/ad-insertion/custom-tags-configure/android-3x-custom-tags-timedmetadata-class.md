---
description: When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process and expose the tag in the form of a TimedMetadata object.
title: Timed metadata class
exl-id: abb552d0-42f9-495e-a307-1f03d6a0b965
---
# Timed metadata class {#timed-metadata-class}

When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process and expose the tag in the form of a TimedMetadata object.

 The class provides the following elements: 

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Property </b></th> 
   <th colname="col02" class="entry"> <b> Type </b></th> 
   <th colname="col2" class="entry"> <b> Description </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Unique identifier of the timed metadata. </p> <p>This value is usually extracted from the cue/tag ID attribute. Otherwise, a unique random value is provided. Use <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata </span> </td> 
   <td colname="col02"> Metadata </td> 
   <td colname="col2"> <p>The processed/extracted information from the playlist/manifest custom tag. Use <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2"> <p>The name of the timed metadata. If the type is <span class="codeph"> TAG </span>, the value represents the cue/tag name. If the type is <span class="codeph"> ID3 </span>, it is null. Use <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>The time position, in milliseconds, relative to the start of the main content where this timed metadata is present in the stream. Use <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Type </td> 
   <td colname="col2"> <p>The type of the timed metadata. Use <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indicates that the timed metadata was created from a tag in the playlist/manifest. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indicates that the timed metadata was created from an ID3 tag in the media stream. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Remember the following:

* TVSDK automatically extracts the attributes list into key-value pairs and stores the attributes in the metadata property. 

  >[!TIP]
  >
  >Complex data in custom tags in the manifest, such as strings with special characters, must be in quotes. For example:
  >
  >```
  >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
  >"www.example.com:8090?parameter1=xyz&parameter2=abc"
  >```
  >

* If the extraction fails because of a custom tag format, the metadata property will be empty and your application must extract the actual information. In this case, no error is thrown.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Element </b></th> 
   <th colname="col2" class="entry"> <b>Description</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public enum Type {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Possible types for the timed metadata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(Type type, long time, long id, String name, Metadata metadata); </span> </td> 
   <td colname="col2"> <p>Default constructor (time is the local stream time). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>The time position, relative to the start of the main content, where this metadata was inserted in the stream. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>The metadata inserted in the stream. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Returns the type of the timed metadata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Returns the ID extracted from the cue/tag attributes. Otherwise, a unique random value is provided. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>Returns the name of the cue, which is usually the HLS tag name. </p> </td> 
  </tr> 
 </tbody> 
</table>
