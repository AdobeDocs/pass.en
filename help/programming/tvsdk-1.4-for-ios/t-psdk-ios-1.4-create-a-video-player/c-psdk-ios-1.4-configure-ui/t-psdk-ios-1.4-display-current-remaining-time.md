---
description: You can display the current and remaining time of the content that is being played.
title: Display the current time and remaining time
exl-id: 61043b2c-949e-494a-9b93-9cf5104d5bde
---
# Display the current time and remaining time {#display-the-current-time-and-remaining-time}

You can display the current and remaining time of the content that is being played.

1. To implement a display that shows the current and remaining time of the active content, use the following sample code:

      ```    
      // 1. Register for the PTMediaPlayerTimeChangeNotification 
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
        name:PTMediaPlayerTimeChangeNotification object:self.player]; 
       
      ... 
       
      // 2. Create labels for displaying current and remaining time 
      _timeCurrentLabel = [[UILabel alloc] initWithFrame:CGRectMake(50.0, 16.0, 50.0, 21.0)]; 
      _timeCurrentLabel.text = @"00:00:00"; 
      _timeCurrentLabel.font = [UIFont boldSystemFontOfSize:12.0]; 
      _timeCurrentLabel.numberOfLines = 1; 
      _timeCurrentLabel.textAlignment = UITextAlignmentCenter; 
      _timeCurrentLabel.backgroundColor = [UIColor clearColor]; 
      _timeCurrentLabel.textColor =  
        [UIColor colorWithRed:209.0/255.0 green:209.0/255.0 blue:209.0/255.0 alpha:1.0]; 
      [self addSubview:_timeCurrentLabel]; 
       
      _timeRemainingLabel = [[UILabel alloc] initWithFrame:CGRectMake(485.0, 16.0, 50.0, 21.0)]; 
      _timeRemainingLabel.text = @"00:00:00"; 
      _timeRemainingLabel.font = [UIFont boldSystemFontOfSize:12.0]; 
      _timeRemainingLabel.numberOfLines = 1; 
      _timeRemainingLabel.textAlignment = UITextAlignmentCenter; 
      _timeRemainingLabel.backgroundColor = [UIColor clearColor]; 
      _timeRemainingLabel.textColor =  
        [UIColor colorWithRed:209.0/255.0 green:209.0/255.0 blue:209.0/255.0 alpha:1.0]; 
       
      ... 
       
      // 3. This method is called whenever the player time changes  
      (PTMediaPlayerTimeChangeNotification) - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
          //The seekable range provides the playback range of a stream  
          CMTimeRange seekableRange = self.player.seekableRange; 
       
          //Verify if the seekableRange is a valid CMTimeRange  
          if (CMTIMERANGE_IS_VALID(seekableRange)) { 
              double  duration = CMTimeGetSeconds(seekableRange.duration); 
              double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime);  
              if (CMTIME_IS_INDEFINITE(self.player.currentItem.duration)) { 
                  //If the duration is indefinite then the content is live.  
                  [_timeCurrentLabel setText:[NSString stringWithFormat:@"--:--"]];  
                  [_timeRemainingLabel setText:[NSString stringWithFormat:@"Live"]]; 
              } 
              else { 
                  [_timeCurrentLabel setText:[self timeFormatter:currentTime]];  
                  [_timeRemainingLabel setText:[self timeFormatter:(duration - currentTime)]]; 
              } 
          } 
      } 
      
      ```

1. To implement a display that show the progress of an ad and the remaining time, use the following sample code:

      ```    
      double adBreakDurationLeft; 
      double adBreakDuration; 
      float currentAdPosition; 
      (void)onMediaPlayerAdBreakStarted:(NSNotification *) notification 
      { 
      PTAdBreak *adBreak = [notification.userInfo objectForKey:PTMediaPlayerAdBreakKey]; 
      self.adBreakDuration = CMTimeGetSeconds(adBreak.range.duration); 
      self.adBreakDurationLeft = self.adBreakDuration; 
      } 
      (void)onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
      { 
      self.adBreakDuration = 0.0f; 
      self.adBreakDurationLeft = 0.0f; 
      } 
      (void)onMediaPlayerAdPlayStarted:(NSNotification *) notification 
      { 
      self.currentAdPosition = 0; 
      } 
      (void)onMediaPlayerAdPlayProgress:(NSNotification *) notification 
      { 
      PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
      CMTime progress = [(NSValue *)[notification.userInfo objectForKey:PTMediaPlayerAdProgressKey] CMTimeValue]; 
      if (ad != nil) { // remaining ad playback time in milliseconds self.currentAdPosition = CMTimeGetSeconds(progress); double timeLeft = self.adBreakDurationLeft - (double)self.currentAdPosition; float currentprogress = 1.0f - (timeLeft/self.adBreakDuration); }  
      } 
      (void)onMediaPlayerAdPlayCompleted:(NSNotification *) notification 
      { 
      PTAd *ad = [notification.userInfo objectForKey:PTMediaPlayerAdKey]; 
      self.adBreakDurationLeft = self.adBreakDurationLeft - ad.primaryAsset.duration; 
      }
      ```

<!--<a id="example_D2FC658F27FC42A0B3E1AEC99B36788B"></a>-->
