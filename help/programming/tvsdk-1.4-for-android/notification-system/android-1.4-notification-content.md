---
description: MediaPlayerNotification objects provide information about changes in player state, warnings, and errors. Errors that stop the playback of the video also cause a change in the state of the player.
title: Notification content
exl-id: b8298865-0389-4610-b495-b8735ef9cd56
---
# Notification content {#notification-content}

MediaPlayerNotification objects provide information about changes in player state, warnings, and errors. Errors that stop the playback of the video also cause a change in the state of the player.

Your application can retrieve the notification and state information. You can also create a logging system for diagnostics and validation by using the notification information.

You implement event listeners to capture and respond to events. Many events provide `MediaPlayerNotification` status notifications.

`MediaPlayerNotification` provides information that is related to the player's status.

TVSDK provides a chronological list of `MediaPlayerNotification` notifications. Each notification contains the following information:

* Time stamp 
* Diagnostic metadata that consists of the following elements:

    * `type`: INFO, WARN, or ERROR. 
    * `code`: A numerical representation of the notification. 
    * `name`: A human-readable description of the notification, such as SEEK_ERROR 
    * `metadata`: Key/value pairs that contain relevant information about the notification. For example, a key named `URL` provides a value that is a URL related to the notification. 
    
    * `innerNotification`: A reference to another `MediaPlayerNotification` object that directly impacts this notification.

You can store this information locally for later analysis or send it to a remote server for logging and graphical representation.

## Set up your notification system {#set-up-your-notification-system}

You can listen for notifications and you can add your own notifications to the notification history.

 The core of the Primetime Player notification system is the `Notification` class, which represents a standalone notification.

The `NotificationHistory` class provides a mechanism for accumulating notifications. It stores a log of notification (NotificationHistoryItem) objects that represents a collection of Notifications.

To receive notifications:

* Listen for notifications 
* Add notifications to the notification history

1. Listen for state changes.
1. Implement the `MediaPlayer.PlaybackEventListener.onStateChanged` callback.
1. TVSDK passes two parameters to the callback:

    * The new state ( `MediaPlayer.PlayerState`) 
    * A `MediaPlayerNotification` object

## Add real-time logging and debugging {#add-real-time-logging-and-debugging}

You can use notifications to implement real-time logging in your video application.

The notification system allows you to gather logging and debugging information for diagnostics and validation without overly stressing the system.

>[!IMPORTANT]
>
>The logging back end is not part of a production setup and is not expected to handle high-load traffic. If your implementation does not need to be absolutely complete, consider the efficiency of data transmission to avoid overloading your system.

Here is an example of how to retrieve notifications. 

1. Create a timer-based execution thread for your video application that periodically queries the data gathered by the TVSDK notification system.

1. If the timer's interval is too large and the size of the event list is too small, the notification event list will overflow. To avoid this overflow, do one of the following:

    * Decrease the time interval that drives the thread that polls for new events. 
    * Increase the size of the notification list.

1. Serialize the latest notification event entries in JSON format and send the entries to a remote server for postprocessing.

   The remote server could then graphically display the provided data in real-time.
1. To detect the loss of notification events, look for gaps in the sequence of event index values.

   Each notification event has an index value that is automatically incremented by the `session.NotificationHistory` class.

## ID3 tags {#id-tags}

ID3 tags provide information about an audio or video file, such as the title of the file or the name of the artist. TVSDK detects ID3 tags at the transport stream (TS) segment level in HLS streams and dispatches an event. The application can extract data from the tag.

>[!IMPORTANT]
>
>TVSDK recognizes ID3 metadata (version 2.3.0 or 2.4.0) in audio (AAC) and video (H.264) streams, in any of its possible encodings (ASCII, UTF8, UTF16-BE, or UTF16-LE). It ignores ID3 tags that are not in one of the recognized versions or formats. Unspecified encoding is treated as UTF8.

When TVSDK detects ID3 metadata, it issues a notification with the following data:

* InfoCode = 303007 
* TYPE = ID3 
* NAME = not present 
* ID = 0

1. Implement an event listener for `MediaPlayer.PlaybackEventListener#onTimedMetadata(TimeMetadata timeMetadata)` and register it with the `MediaPlayer` object.

   TVSDK calls this listener when it detects ID3 metadata.

   >[!NOTE]
   >
   >Custom ad cues use the same `onTimedMetadata` event to indicate detection of a new tag. This should not cause any confusion because custom ad cues are detected at the manifest level, and ID3 tags are embedded in the stream. For more information, see  custom-tags-configure .

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
               String value = metadata.getValue(key); 
           } 
       } 
   }
   ```
