---
description: When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it in the form of a PTTimedMetadata object.
title: Timed metadata class
exl-id: b619b019-cb6d-4c31-a7e2-7ebe2f44a4b0
---
# Timed metadata class{#timed-metadata-class}

When TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it in the form of a PTTimedMetadata object.

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
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> Unique identifier of the timed metadata. This value is usually extracted from the cue/tag ID attribute. Otherwise, a unique random value is provided. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> The name of the timed metadata. If the type is <span class="codeph"> TAG</span>, the value represents the cue/tag name. If the type is <span class="codeph"> ID3</span>, it is null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> The time position, in milliseconds, relative to the start of the main content where this timed metadata is present in the stream. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
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

* If the extraction fails because of a custom tag format, the content property always contains the tag's raw data, which is the string after the colon. No error is thrown in this case.

|  Element  | Description  |
|---|---|
|  TAG, ID3  | Possible types for the timed metadata.  |
| `@property (nonatomic, assign) CMTime time`  | The time position, relative to the start of the main content, where this metadata was inserted in the stream.  |
| `@property (nonatomic, assign) PTTimedMetadataType type`  | Returns the type of the timed metadata.  |
| `@property (nonatomic, retain) NSString *metadataId`  | Returns the ID extracted from the cue/tag attributes. Otherwise, a unique random value is provided.  |
| `@property (nonatomic, retain) NSString *name`  | Returns the name of the cue, which is usually the HLS tag name.  |
