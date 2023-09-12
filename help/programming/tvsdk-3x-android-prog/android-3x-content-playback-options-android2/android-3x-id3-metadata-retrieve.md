---
description: ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. TVSDK detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.
title: ID3 tags
exl-id: 7db9150d-bb1d-4e93-84c1-04a1f6605bdc
---
# ID3 tags {#id-tags}

ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. TVSDK detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.

>[!IMPORTANT]
>
>TVSDK recognizes ID3 metadata (version 2.3.0 or 2.4.0) in audio (AAC) and video (H.264) streams in any of its possible encodings (ASCII, UTF8, UTF16-BE, or UTF16-LE). It ignores ID3 tags that are not in one of the recognized versions or formats. Unspecified encoding is treated as UTF8.

When TVSDK detects ID3 metadata, it issues a notification with the following data:

* TYPE = ID3 
* NAME = ID3

1. Implement an event listener for `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` and register it with the `MediaPlayer` object.

   TVSDK calls this listener when it detects `ID3` metadata.

   >[!TIP]
   >
   >Custom ad cues use the same `onTimedMetadata` event to indicate detection of a new tag. This should not cause any confusion because custom ad cues are detected at the manifest level, and ID3 tags are embedded in the stream. For more information, see [Custom tags](../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/custom-tags-configure/android-3x-custom-tags-configure.md).

1. Retrieve the metadata.

   ```java
   @Override 
    public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```
