---
description: To receive notifications about tags in the manifest, implement the appropriate notification listener(s).
title: Add listeners for timed metadata notifications
exl-id: 30606188-ee0e-419d-96af-3571c8836422
---
# Add listeners for timed metadata notifications {#add-listeners-for-timed-metadata-notifications}

To receive notifications about tags in the manifest, implement the appropriate notification listener(s).

You can monitor timed metadata by listening for the following events, which notify your application of related activity:

* `PTTimedMetadataChangedNotification`: Each time a unique subscribed tag is identified during parsing of the content, TVSDK prepares a new `PTTimedMetadata` object and dispatches this notification.

  The object contains the name of the tag to which you subscribed, the local time in the playback where this tag will appear, and other data. 

* `PTMediaPlayerTimeChangeNotification` : For live/linear streams where the manifest/playlist refreshes periodically, additional custom tags might appear in the updated playlist/manifest, so additional `TimedMetadata` objects might be added to the `MediaPlayerItem.timedMetadata` property.

  This event notifies your application when this happens.

   Retrieve the timed metadata in one of the following ways.

    * Set your application to add itself as a listener to the `PTTimedMetadataChangedNotification` notification and fetch the object using `PTTimedMetadataKey`.     
    
      ```    
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
       
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

    * Access the `timedMetadataCollection` property of `PTMediaPlayerItem`, which consists of all the `PTTimedMetadata` objects that have been notified so far.
