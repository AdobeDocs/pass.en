---
title: Enable background audio
description: Enable background audio
copied-description: yes
exl-id: 5bb72233-27d0-4968-b32c-c8d5ac5ac8c8
---
# Enable background audio {#enable-background-audio}

To enable audio playback when app is in background, app should call `enableAudioPlaybackInBackground` API of MediaPlayer with true as argument when player is in PREPARED state.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

App should pause playback when it loses its hold on audio focus during events like responding to the phone, etc. The following code snippet demonstrates how to implement the `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
