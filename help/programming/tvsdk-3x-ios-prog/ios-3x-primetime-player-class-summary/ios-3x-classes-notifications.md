---
description: These classes describe messages about errors, warnings, and some activities that the TVSDK issues for logging and debugging purposes.
title: Notification classes
exl-id: 97a01418-f747-4a6e-bfa5-e680438e40c5
---
# Notification classes {#notification-classes}

These classes describe messages about errors, warnings, and some activities that the TVSDK issues for logging and debugging purposes.

|  **Class name**  | **Description**  |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html)  |Class that describes the notification for an error that causes the player to stop playback. This is a [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) of notification type ERROR.  |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html)  | Lists all the notifications dispatched by the Primetime Player framework.  |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)  |Class that provides informational messages, warnings, and errors. Encapsulates the object representation of a single notification event within [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html).  |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)  |Class that stores a log of notification objects [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) objects that provides access to a notification events history list. That is, it maintains a list of elements, each element containing a separate instance of the [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)  |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html)  |Class that defines an entry in the circular list in [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) and holds the notification and its timestamp.  |
