---
description: ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. Browser TVSDK detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.
title: ID3 tags
exl-id: 33510821-9de4-41fc-b404-bcf0b6ba86ff
---
# ID3 tags{#id-tags}

ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. Browser TVSDK detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.

When a new ID3 metadata is found in the underlying HLS stream, Browser TVSDK triggers an `AdobePSDK.TimedMetadataEvent` event.

The `TimedMetadata` object for ID3 has the following properties:  

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Property Name </th> 
   <th colname="col2" class="entry"> Details </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type </span> </p> </td> 
   <td colname="col2"> <p>A type of <span class="codeph"> TimedMetadata </span> object. </p> <p>For ID3 metadata, the value is <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> time </span> </p> </td> 
   <td colname="col2"> <p> The player time where this timed metadata was detected. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID of the <span class="codeph"> TimedMetadata </span> object. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name </span> </p> </td> 
   <td colname="col2"> <p>Name of <span class="codeph"> TimedMetadata </span> object. For ID3 metadata, the value is "ID3". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> content </span> </p> </td> 
   <td colname="col2"> <p>The timed metadata content. For ID3 tags, this value represents the serialized byte array. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> metadata </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> processed information, which is an instance of <span class="codeph"> AdobePSDK.Metadata </span> where the ID3 frames are stored. </p> <p> <p>Note:  For Safari <span class="codeph"> video </span> tag, ID3 tag's particular frame data is exposed in the form of object through an <span class="codeph"> AdobePSDK.Metadata </span> object whereas for other browsers, ID3 tag's frame data is exposed in the form of a byte array through <span class="codeph"> AdobePSDK.Metadata </span> object. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

​

The various ID3 tags that are stored in `TimedMetadata` can be retrieved by the application in the following two ways:

* In AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE event listener.

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var mediaPlayer = new AdobePSDK.MediaPlayer(); 
  mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
      var td = event.timedMetadata; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  }); 
  ```

* Using the `MediaPlayerItem`'s `timedMetadata` property. 

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var timedMetadataList = player.currentItem.timedMetadata; 
  for(var i = 0; i < timedMetadataList.length; i++){ 
      var td = timedMetadataList[i]; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  } 
  ```
