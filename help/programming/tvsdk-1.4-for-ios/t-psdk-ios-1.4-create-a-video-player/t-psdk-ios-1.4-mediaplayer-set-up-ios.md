---
description: The PTMediaPlayer interface encapsulates the functionality and behavior of a media player object.
title: Set up the PTMediaPlayer
exl-id: cf8f46c8-c52a-4f44-b493-965ce1b50c68
---
# Set up the PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK provides tools for creating an advanced video player application (your Primetime player), which you can integrate with other Primetime components.

Use your platform's tools to create a player and connect it to the media player view in TVSDK, which has methods to play and manage videos. For example, TVSDK provides play and pause methods. You can create user interface buttons on your platform and set the buttons to call those TVSDK methods.

The PTMediaPlayer interface encapsulates the functionality and behavior of a media player object.

To set up your `PTMediaPlayer`: 

1. Fetch the media's URL from your user interface, for example, in a text field.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Create `PTMetadata`.

   Assume that your method `createMetada` prepares metadata (see [Advertising](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Create `PTMediaPlayerItem` by using your `PTMetadata` instance.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Add observers to notifications that TVSDK dispatches.

   ```
   [self addObservers]
   ```

1. Create `PTMediaPlayer` using your new `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Set properties on your player.

   Here are some of the available `PTMediaPlayer` properties: 

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Set the player's view property.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
    
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Add the player's view in the current view's subview.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Call `play` to start media playback.

   ```
   [player play];
   ```
