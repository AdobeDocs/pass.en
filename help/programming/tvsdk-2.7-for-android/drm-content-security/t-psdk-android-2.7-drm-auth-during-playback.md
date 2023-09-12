---
description: When the DRM metadata for a video is included in the media stream, you can perform authentication during playback.
title: DRM authentication during playback
exl-id: f6e6e73a-d455-4b2c-b35c-2db173372092
---
# DRM authentication during playback {#drm-authentication-during-playback}

When the DRM metadata for a video is included in the media stream, you can perform authentication during playback.

With license rotation, an asset is encrypted with multiple DRM licenses. Each time that new DRM metadata is discovered, the `DRMHelper` methods are used to check whether the DRM metadata requires DRM authentication.

>[!TIP]
>
>Before starting playback, determine whether you are dealing with a domain bound license and whether domain authentication is required. If yes, complete the domain authentication and join the domain.

1. When new DRM Metadata is discovered in an asset, an event is dispatched at the application layer.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
    
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. Use the `DRMMetadata` to check whether authentication is needed.

    * If authentication is not required, you do not need to do anything, and playback continues uninterrupted. 
    * If authentication is required, complete DRM authentication.

      Since this operation is asynchronous and is handled in a different thread, it has no impact on the user interface nor on video playback.

1. If authentication fails, the user cannot continue viewing the video, and playback stops.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

For example: 

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
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
