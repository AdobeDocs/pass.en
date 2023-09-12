---
description: These classes describe messages about errors, warnings, and some activities that the issues for logging and debugging purposes.
title: Notification classes
exl-id: d8af783f-1e80-4e50-89b8-97643ff6670b
---
# Notification classes {#notification-classes}

These classes describe messages about errors, warnings, and some activities that the issues for logging and debugging purposes.

 Package: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html) 

|  Class name  | Description  |
|---|---|
| [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html)  |Class that provides informational messages, warnings, and errors. Encapsulates the object representation of a single notification event within [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html).  |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html)  | Returns the description associated with the provided notification codeand provides numeric constants for notification objects.  |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)  |Class that stores a log of notification objects. A circular list of [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) objects that provides access to a notification events history list. That is, it maintains a list of elements, each element containing a separate instance of the [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) class.  |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html)  |Class that defines an entry in the circular list in [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) and holds the notification and its timestamp.  |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html)  | Class that contains the supported notifications types.  |
