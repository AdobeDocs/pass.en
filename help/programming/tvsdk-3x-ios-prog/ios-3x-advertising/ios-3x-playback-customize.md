---
description: When playback reaches an ad break, passes an ad break, or ends in an ad break, TVSDK defines some default behavior for the positioning of the current playhead.
title: Customize playback with ads
exl-id: 522f0b55-dcc4-4175-91ab-757b72bbad23
---
# Customize playback with ads {#customize-playback-with-ads}

When playback reaches an ad break, passes an ad break, or ends in an ad break, TVSDK defines some default behavior for the positioning of the current playhead.

>[!TIP]
>
>You can override the default behavior by using the `PTAdPolicySelector` class.

The default behavior varies, depending on whether the user passes the ad break during normal playback or by seeking in a video.

You can customize ad playback behavior in the following ways:

* Save the position where the user stopped watching the video and resume playing at the same position in a future session. 
* If an ad break is presented to the user, display no additional ads for a number of minutes, even if the user seeks to a new position. 
* If the content fails to play after a few minutes, restart the stream or fail over to a different source for the same content.

  On the failover playback session, to allow the user to skip ads and resume to the previous failed position, you can disable pre-roll and/or mid-roll ads. TVSDK provides methods to enable skipping pre-roll and mid-roll ads.

## API elements for ad playback {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK provides classes and methods you can use to customize the playback behavior of content that contains advertising. 
The following API elements are useful for customizing playback: 

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API element</b></th> 
   <th colname="col2" class="entry"><b>Content that supports advertising</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Control whether an ad break should be marked as having been watched by a viewer, and if yes, when to mark it. Set and get the watched policy using <span class="codeph"> adBreakAsWatched </span> property. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocol that allows customization of TVSDK ad behavior. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Class that implements the default TVSDK behavior. Your application can override this class to customize the default behaviors without implementing the complete interface. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>This is the local time of the playback, excluding the placed ad breaks. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>Here, the seek occurs relative to a local time in the stream. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>The virtual position on the timeline is converted to the local position. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> property. Indicates whether the viewer has watched the ad. </td> 
  </tr> 
 </tbody> 
</table>

## Set up customized playback {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Before you can customize or override ad behaviors, register the ad policy instance with TVSDK.

To customize ad behaviors, do one of the following:

* Conform to the `PTAdPolicySelector` protocol and implement all the required policy selection methods.

  This option is recommended if you need to override **all** the default ad behaviors. 

* Override the `PTDefaultAdPolicySelector` class and provide implementations for only those behaviors that require customization.

  This option is recommended if you need to override only **some** of the default behaviors.

For both options, complete the following tasks:

1. Register the policy instance to be used by TVSDK through the client factory. 

   >[!NOTE]
   >
   >Custom ad policies that are registered at the beginning of playback are cleared when the `PTMediaPlayer` instance is deallocated. Your application must register a policy selector instance each time a new playback session is created.

   For example:  

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
     
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implement your customizations.

## Skip ad breaks for a period of time {#section_99809BE4D9BB4DEEBBF596C746CA428A}

By default, TVSDK forces an ad break to play when the user seeks over an ad break. You can customize the behavior to skip an ad break if the time elapsed from a previous break completion is within a certain number of minutes.

>[!IMPORTANT]
>
>When there is an internal seek to skip an ad, here might be a slight pause in the playback.

The following example of a customized ad policy selector skips ads in the next five minutes (wall clock time) after a user has watched an ad break.

1. Register the policy instance to be used by TVSDK through the client factory. 

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
     
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implement your customization.

**PTS5MinuteSkipBreakPolicySelector.h** 

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m** 

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## Save the video position and resume later {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

You can save the current playback position in a video and resume playing at the same position in a future session.

Dynamically inserted ads differ between user sessions, so saving the position **with** spliced ads refers to a different position in a future session. TVSDK provides methods to retrieve the playback position while ignoring spliced ads.

1. When the user quits a video, your application retrieves and saves the position in the video. 

   >[!TIP]
   >
   >Ad durations are not included.

   Ad breaks can vary in each session due to ad patterns, frequency capping, and so on. The current time of the video in one session might be different in a future session. When saving a position in the video, the application retrieves the local time  . Use the  `localTime` property  to read this position , which you can save on the device or in a database on the server.

   For example, if the user is at the 20th minute of the video, and this position includes five minutes of ads, `currentTime` will be 1200 seconds, while `localTime` at this position will be 900 seconds.

   >[!IMPORTANT]
   >
   >Local time and current time are the same for live/linear streams. In this case, `convertToLocalTime` has no effect. For VOD, local time remains unchanged while ads play.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
        
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. To resume the video at the same position that was saved from the previous session, use `seekToLocalTime`. 

   >[!TIP]
   >
   >This method is called only with local time values. If the method is called with current time results, incorrect behavior occurs.

   To seek to the current time, use `seekToTime`. 

1. When your application receives the `PTMediaPlayerStatusReady` status change event, seek to the saved local time. 

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Provide the ad breaks as specified in the ad policy interface. 
1. Implement a custom ad policy selector by extending the default ad policy selector. 
1. Provide the ad breaks that must be presented to the user by implementing `selectAdBreaksToPlay` 

   >[!NOTE]
   >
   >This method includes a pre-roll ad break and the mid-roll ad breaks before the local time position. Your application can decide to play a pre-roll ad break and resume to the specified local time, play a mid-roll ad break and resume to the specified local time, or play no ad breaks.
