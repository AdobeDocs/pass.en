---
description: MediaPlayerStatus objects provide information about changes in player status. Notification objects provide information about warnings and errors. Errors that stop the playback of the video also cause a change in the status of the player. You implement event listeners to capture and respond to events (MediaPlayerEvent objects).
title: Notifications and events for player status, activity, errors, and logging
exl-id: c25e834e-ffa0-444c-9285-331e6841ac29
---
# Notifications and events for player status, activity, errors, and logging {#notifications-and-events-for-player-status-activity-errors-and-logging}

Events and notifications help you manage the asynchronous aspects of the video application.

MediaPlayerStatus objects provide information about changes in player status. Notification objects provide information about warnings and errors. Errors that stop the playback of the video also cause a change in the status of the player. You implement event listeners to capture and respond to events (MediaPlayerEvent objects).

Your application can retrieve notification and status information. Using this information, you could also create a logging system for diagnostics and validation.

## Notification content {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` provides information that is related to the player's status.

TVSDK provides a chronological list of `MediaPlayerNotification` notifications, and each notification contains the following information:

* A time stamp 
* Diagnostic metadata that consists of the following elements:

    * `type`: INFO, WARN, or ERROR. 
    * `code`: A numerical representation of the notification. 
    * `name`: A human-readable description of the notification, such as SEEK_ERROR 
    * `metadata`: Key/value pairs that contain relevant information about the notification. For example, a key named `URL` provides a value that is a URL related to the notification. 
    
    * `innerNotification`: A reference to another `MediaPlayerNotification` object that directly impacts this notification.

You can store this information locally for later analysis or send it to a remote server for logging and graphical representation.

## Set up your notification system {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

You can listen for notifications.

The core of the Primetime Player notification system is the `Notification` class, which represents a standalone notification.

To receive notifications, listen for notifications as follows:

1. Implement the `NotificationEventListener.onNotification()` callback. 
1. TVSDK passes a `NotificationEvent` object to the callback. 

   >[!NOTE]
   >
   >Notifications types are enumerated in the `Notification.Type` enum:

    * `ERROR` 
    * `INFO` 
    * `WARNING`

## Add real-time logging and debugging {#section_9D4004308CB243AD9B50818895D10005}

You can use notifications to implement real-time logging in your video application.

The notification system allows you to gather logging and debugging information for diagnostics and validation without stressing the system.

>[!IMPORTANT]
>
>The logging back end is not part of a production setup and is not expected to handle high-load traffic. If your implementation does not need to be absolutely complete, consider the efficiency of data transmission to avoid overloading your system.

Here is an example of how to retrieve notifications:

1. Create a timer-based execution thread for your video application that periodically queries the data gathered by the TVSDK notification system. 
1. If the timer's interval is too large, and the size of the event list is too small, the notification event list will overflow. 

   >[!NOTE]
   >
   >To avoid this overflow, do one of the following:
   >
   >1. Decrease the time interval that drives the thread that polls for new events. 
   >1. Increase the size of the notification list. 
   >

1. Serialize the latest notification event entries in JSON format and send the entries to a remote server for postprocessing. 

   >[!NOTE]
   >
   >The remote server can graphically display the provided data in real-time.

1. To detect the loss of notification events, look for gaps in the sequence of event index values.
