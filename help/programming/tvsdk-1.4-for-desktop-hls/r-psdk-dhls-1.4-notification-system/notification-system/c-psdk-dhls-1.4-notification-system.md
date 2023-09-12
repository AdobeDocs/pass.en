---
description: MediaPlayerNotification objects provide information about changes in player status, warnings, and errors. Errors that stop the playback of the video also cause a change in the status of the player.
title: Notifications for player status, activity, errors, and logging
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
---
# Overview {#notifications-for-player-status-activity-errors-and-logging-overview}

MediaPlayerNotification objects provide information about changes in player status, warnings, and errors. Errors that stop the playback of the video also cause a change in the status of the player.

Your application can retrieve the notification and status information. You can also create a logging system for diagnostics and validation by using the notification information.

You implement event listeners to capture and respond to events. Many events provide `MediaPlayerNotification` status notifications.
