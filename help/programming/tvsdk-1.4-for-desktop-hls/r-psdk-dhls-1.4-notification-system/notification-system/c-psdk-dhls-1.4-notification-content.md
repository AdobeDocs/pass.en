---
description: MediaPlayerNotification provides information that is related to the player's status.
title: Notification content
exl-id: dc46f717-f08b-4d52-82ea-88107076f4fb
---
# Notification content{#notification-content}

MediaPlayerNotification provides information that is related to the player's status.

TVSDK provides a chronological list of `MediaPlayerNotification` notifications. Each notification contains the following information:

* Time stamp 
* Diagnostic metadata that consists of the following elements:

    * type INFO, WARN, or ERROR 
    * `code`: A numerical representation of the notification. 
    * `name`: A human-readable description of the notification, such as SEEK_ERROR 
    * `metadata`: Key/value pairs that contain relevant information about the notification. For example, a key named `URL` provides a value that is a URL related to the notification. 
    
    * `innerNotification`: A reference to another `MediaPlayerNotification` object that directly impacts this notification.

You can store this information locally for later analysis or send it to a remote server for logging and graphical representation.
