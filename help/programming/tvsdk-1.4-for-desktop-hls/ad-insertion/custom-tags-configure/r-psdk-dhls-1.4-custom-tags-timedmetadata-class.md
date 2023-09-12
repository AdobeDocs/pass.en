---
description: When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it in the form of a TimedMetadata object.
title: Timed metadata class
exl-id: bf2bf78d-9063-4f54-97d9-60238b77ee93
---
# Timed metadata class{#timed-metadata-class}

When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it in the form of a TimedMetadata object.

 The class provides the following elements: 

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Property </th> 
   <th colname="col02" class="entry"> Type </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> content</span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2"> The raw content of the timed metadata. If the type is TAG, the value represents the entire attribute list of the cue/tag. If the type id ID3, it is null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2"> Unique identifier of the timed metadata. This value is usually extracted from the cue/tag ID attribute. Otherwise, a unique random value is provided. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> metadata</span> </td> 
   <td colname="col02"> Metadata </td> 
   <td colname="col2"> The processed/extracted information from the playlist/manifest custom tag. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2">The name of the timed metadata. If the type is <span class="codeph"> TAG</span>, the value represents the cue/tag name. If the type is <span class="codeph"> ID3</span>, it is null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"> Number </td> 
   <td colname="col2"> The time position, in milliseconds, relative to the start of the main content where this timed metadata is present in the stream. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> String </td> 
   <td colname="col2">The type of the timed metadata. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indicates that the timed metadata was created from a tag in the playlist/manifest. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indicates that the timed metadata was created from an ID3 tag in the media stream. </li> 
    </ul> </td> 
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

* If the extraction fails because of a custom tag format, the metadata property will be empty and your application must extract the actual information. No error is thrown in this case.

|  Element  | Description  |
|---|---|
| `TAG, ID3 ID3, TAG`  | Possible types for the timed metadata.  |
|  `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)`  | Default constructor (time is the local stream time).  |
| `content:String`  | The raw content of the source tag of this timed metadata.  |
| `time:Number`  | The time position, relative to the start of the main content, where this metadata was inserted in the stream.  |
|  `metadata:Metadata`  | The metadata inserted in the stream.  |
| `type:String`  | Returns the type of the timed metadata.  |
| `id:String`  | Returns the ID extracted from the cue/tag attributes. Otherwise, a unique random value is provided.  |
| `name:String`  | Returns the name of the cue, which is usually the HLS tag name.  |
