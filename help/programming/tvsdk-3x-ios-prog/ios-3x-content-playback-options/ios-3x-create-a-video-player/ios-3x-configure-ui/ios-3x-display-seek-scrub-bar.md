---
description: You can display the current and remaining time of the content that is being played.
title: Display a seek scrub bar with the current playback time position
exl-id: 2093ee96-84fe-4011-ba18-275f2bf960ca
---
# Display a seek scrub bar with the current playback time position {#display-a-seek-scrub-bar-with-the-current-playback-time-position}

You can display the current and remaining time of the content that is being played.

   To implement a scrub bar, use the following sample code:

   ```
   // 1. Register for the PTMediaPlayerTimeChangeNotification 
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
     name:PTMediaPlayerTimeChangeNotification object:self.player]; 
    
   ... 
    
   _positionSlider = [[UISlider alloc] initWithFrame:CGRectMake(105.0, 14.0, 370, 24)];  
   [_positionSlider addTarget:self action:@selector(sliderThumbReleased:)  
     forControlEvents:UIControlEventTouchUpInside]; 
    
   ... 
    
   // 2. Cover the event where the user moves to a different location in the stream 
   - (void)sliderThumbReleased:(id)sender { 
       double  sliderTime = [_positionSlider  value];  
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double start = CMTimeGetSeconds(seekableRange.start);  
           double duration = CMTimeGetSeconds(seekableRange.duration); 
    
           CMTime newTime = CMTimeMakeWithSeconds((sliderTime * duration) + start, AD_TIMESCALE);  
           [self.player seekToTime:newTime]; 
       } 
   } 
    
   ... 
    
   // 3. This method is called whenever the player time changes  
   (PTMediaPlayerTimeChangeNotification) 
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
    
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double start = CMTimeGetSeconds(seekableRange.start);  
           double duration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime); 
    
           if (duration > 0) { 
               //Set the position slider value on the current playback time  
               [_positionSlider setValue:((currentTime - start) / duration)]; 
           } 
       } 
   } 
   
   ```
