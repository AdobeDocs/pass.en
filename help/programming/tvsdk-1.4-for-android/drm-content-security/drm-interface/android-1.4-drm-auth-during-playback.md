---
description: When the DRM metadata for a video is included in the media stream, perform authentication during playback.
title: DRM authentication during playback
exl-id: 3f190d37-291e-4a5e-811d-7e9984a6a44a
---
# DRM authentication during playback {#drm-authentication-during-playback}

When the DRM metadata for a video is included in the media stream, perform authentication during playback.

Consider the license rotation feature, where an asset is encrypted with multiple DRM licenses. Each time that new DRM metadata is discovered, use `DRMHelper` methods to check whether the DRM metadata requires DRM authentication.

>[!NOTE]
>
>This tutorial does not handle domain bound licenses. Ideally, before starting playback, check whether you are dealing with a domain bound license. If yes, perform domain authentication (if needed) and join the domain.

1. When new DRM Metadata is discovered in an asset, an event is dispatched at the application layer.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
    
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. Use the `DRMMetadata` to check whether authentication is needed. If not, do nothing; playback continues uninterrupted.
1. Otherwise, perform DRM authentication. Since this operation is asynchronous and is handled in a different thread, it has no impact on the user interface nor on video playback.
1. If authentication fails, the user cannot continue viewing the video, and playback ceases. Otherwise, playback will continue uninterruptedly.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
        }); 
    } 
};
```
