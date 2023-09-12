---
description: To receive notifications about tags in the manifest, you need to implement the appropriate event listeners.
title: Add listeners for timed metadata notifications
exl-id: e38f2a25-3379-4132-a8de-6703dc564ed4
---
# Add listeners for timed metadata notifications {#add-listeners-for-timed-metadata-notifications}

To receive notifications about tags in the manifest, you need to implement the appropriate event listeners.

You can monitor timed metadata by listening for `onTimedMetadata`, which notify your application of related activity. Each time a unique subscribed tag is identified during parsing of the content, TVSDK prepares a new `TimedMetadata` object and dispatches this event. The object contains the name of the tag to which you subscribed, the local time in the playback where this tag will appear, and other data. 

1. Listen for events.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
    
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   
   ```

ID3 metadata uses the same `onTimedMetadata` listener to indicate the presence of an ID3 tag. This should not cause any confusion, however, because you can use the `TimedMetadata` `type` property to differentiate between TAG and ID3. For more information about ID3 tags, see  [ID3 tags](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md).
