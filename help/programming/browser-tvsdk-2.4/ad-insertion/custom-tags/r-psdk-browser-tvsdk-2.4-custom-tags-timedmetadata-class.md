---
description: When Browser TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it as a TimedMetadata object.
title: Timed metadata class
exl-id: 893879b5-03ed-4c11-80a6-b57b7d54a95c
---
# Timed metadata class{#timed-metadata-class}

When Browser TVSDK detects a subscribed tag in the playlist/manifest, the player automatically tries to process the tag and expose it as a TimedMetadata object.

The `TimedMetadata` class provides the following elements: 

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Property </th> 
   <th colname="col02" class="entry"> Type </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Here are the timed metadata types: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG - the timed metadata was created from a tag in the playlist/manifest. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - the timed metadata was created from a ID3 tag in the media stream. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>time </p> </td> 
   <td colname="col02"> <p>Number </p> </td> 
   <td colname="col2"> <p>The local time position (milliseconds) relative to the start of the main content where this timed metadata is present in the stream. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>The unique identifier of the timed metadata. </p> <p>Is usually extracted from the cue/tag ID attribute if present. Otherwise, it is a unique random value. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Number </p> </td> 
   <td colname="col2"> <p>The name of the timed metadata. </p> <p>If the type is TAG, the value represents the cue/tag name. If the type is ID3, the value is null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>content </p> </td> 
   <td colname="col02"> <p>String </p> </td> 
   <td colname="col2"> <p>The raw content of the timed metadata. </p> <p>If the type is TAG, the value represents the entire attribute list of the cue/tag. If the type id ID3, the value is null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadata </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadata</span> </p> </td> 
   <td colname="col2"> <p>The processed/extracted information from the playlist/manifest custom tag. </p> </td> 
  </tr> 
 </tbody> 
</table>
