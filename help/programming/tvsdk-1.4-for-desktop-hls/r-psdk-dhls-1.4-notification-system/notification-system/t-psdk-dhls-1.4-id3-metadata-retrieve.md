---
description: ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.
title: ID3 tags
exl-id: 1934516e-729b-476a-a19d-677bf2eb922a
---
# ID3 tags{#id-tags}

ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.

>[!IMPORTANT]
>
>TVSDK recognizes ID3 metadata (version 2.3.0 or 2.4.0) in audio (AAC) and video (H.264) streams, in any of its possible encodings (ASCII, UTF8, UTF16-BE, or UTF16-LE). It ignores ID3 tags that are not in one of the recognized versions or formats. Unspecified encoding is treated as UTF8.

When TVSDK detects ID3 metadata, it issues a notification with the following data:

* InfoCode = 303007 
* TYPE = ID3 
* NAME = not present 
* ID = 0

1. Implement an event listener for `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED` and register it with the `MediaPlayer` object.

   TVSDK calls this listener when it detects ID3 metadata.

   >[!NOTE]
   >
   >Custom ad cues use the same `onTimedMetadata` event to indicate detection of a new tag. This should not cause any confusion because custom ad cues are detected at the manifest level, and ID3 tags are embedded in the stream. For more information, see  custom-tags-configure .

1. Retrieve the metadata.

   ```
   private function onID3Metadata(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       var metadata:Metadata = timedMetadata.metadata; 
       var keys:Vector.<String> = metadata.keySet(); 
       for (var i:int = keys.length - 1; i >= 0; --i) { 
           var value:ByteArray = metadata.getByteArray(keys[i]); 
           _logger.info("#onTimedMetadata Detected dictionary data key: [{0}],  
                        value: [{1}] of length {2} bytes at time [{3}].",  
                        keys[i],  
                        value.toString(),  
                        value.length,  
                        event.timedMetadata.time); 
       } 
   } 
   
   ```
