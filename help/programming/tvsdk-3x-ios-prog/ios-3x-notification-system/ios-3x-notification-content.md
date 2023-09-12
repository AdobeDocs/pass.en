---
description: PTNotification objects provide information about changes in player status, warnings, and errors. Errors that stop the playback of the video also cause a change in the status of the player.
title: Notification content
exl-id: 62423718-b154-4105-82b2-f6e389105ec8
---
# Notifications for player status, activity, errors, and logging {#notifications-player-status-activity-errors-logging}

`PTNotification` objects provide information about changes in player status, warnings, and errors. Errors that stop the playback of the video also cause a change in the status of the player.

Your application can retrieve the notification and status information. You can also create a logging system for diagnostics and validation by using the notification information.

>[!NOTE]
>
>TVSDK also uses *`notification`* to refer to `NSNotifications` ( `PTMediaPlayer` notifications) *`event`* notifications, dispatched to provide information about player activity.

TVSDK also issues `PTMediaPlayerNewNotificationItemEntryNotification` when it issues `PTNotification`.

You implement event listeners to capture and respond to events. Many events provide `PTNotification` status notifications.

## Notification content {#notification-content}

`PTNotification` provides information that is related to the player's status.

TVSDK provides a chronological list of `PTNotification` notifications. Each notification contains the following information:

* Time stamp 
* Diagnostic metadata that consists of the following elements:

    * `type`: INFO, WARN, or ERROR. 
    * `code`: A numerical representation of the notification. 
    * `name`: A human-readable description of the notification, such as SEEK_ERROR 
    * `metadata`: Key/value pairs that contain relevant information about the notification. For example, a key named `URL` provides a value that is a URL related to the notification. 
    
    * `innerNotification`: A reference to another `PTNotification` object that directly impacts this notification.

You can store this information locally for later analysis or send it to a remote server for logging and graphical representation.

## Notification setup {#notification-setup}

TVSDK sets up the player for basic notifications, although you must complete the same set up for your custom notifications.

There are two implementations for `PTNotification`:

* To listen 
* To add custom notifications to `PTNotificationHistory`

To listen to notifications, TVSDK instantiates the `PTNotification` class and attaches it to an instance of the `PTMediaPlayerItem`, which is attached to a PTMediaPlayer instance. There is only one `PTNotificationHistory` instance per `PTMediaPlayer`.

>[!IMPORTANT]
>
>If you are adding customizations, your applications and not TVSDK, must perform those steps.

## Listen to notifications {#listen-to-notifications}

There are two ways to listen to the `PTNotification` notification in the `PTMediaPlayer`:

1. Manually check the `PTNotificationHistory` of the `PTMediaPlayerItem` with a timer and check the differences:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
    
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Use the posted [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) of the `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Register to the `NSNotification` by using the instance of the `PTMediaPlayer` from which you want to get notifications:

   ```
   //Register to the NSNotification 
    
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implement notification callbacks {#implement-notification-callbacks}

You can implement notification callbacks.

   Implement the notification callback by getting the `PTNotification` from the `NSNotification` user information and reading its values by using `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Add custom notifications {#add-custom-notifications}

 To add a custom notification: 
   Create a new `PTNotification` and add it to the `PTNotificationHistory` by using the current `PTMediaPlayerItem`:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
    
   //Create notification 
   PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
    
   //Add notification 
   [notificationHistory addNotification:notification];
   ```
