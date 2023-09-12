---
description: The Primetime player supports Primetime DRM integration as custom DRM workflows. This means that your application must implement the DRM authentication workflows before playing the stream.
title: DRM content protection
exl-id: c1904d15-023f-49fb-95f9-d157d17b3516
---
# DRM content protection {#drm-content-protection}

The Primetime player supports Primetime DRM integration as custom DRM workflows. This means that your application must implement the DRM authentication workflows before playing the stream.

To enable this, TVSDK provides you with the DRM manager for authentication. The reference implementation provides an example of the following workflows:

* How to load and play back HLS streams with Access content protection, optimized for low error rates and quick start up.
* How to load and play back HLS streams with AES128 content protection. 
* How to load and play back HLS streams with PHLS content protection, optimized for low error rates and quick start up.

All DRM-protected content is handled automatically by the DRM libraries built into the TVSDK. However, you can expose error handling, optimization of device individualization, and license acquisition using TVSDK API callbacks.

## Add content protection to the player {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

You can add content protection to the player by creating a playback manager or by using the manager factory.

To create a content protection manager:

* Initialize the DRM system.

  The following code example shows calling `loadDRMServices` in the application `onCreate()` function, to ensure that any initialization required for the DRM system is initiated prior to playback starting.

  ```java
  @Override 
   public void onCreate() { 
       super.onCreate();  
       DrmManager.loadDRMServices(getApplicationContext()); 
   }
  ```

* Preload the DRM licenses.

  The following code example shows loading the `VideoItems` when the content list has finished loading. This will result in the DRM licenses being acquired from the license server and cached locally, so that when playback starts, the content will load with minimum delay.

  ```java
  DrmManager.preLoadDrmLicenses(item.getUrl(),  
    new MediaPlayerItemLoader.LoaderListener() { 
   
      @Override 
      public void onLoadComplete(MediaPlayerItem item) { 
          Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
      } 
   
      @Override 
      public void onError(MediaErrorCode errorCode, String s) { 
          Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
      } 
  } 
  ```

  >[!NOTE]
  >
  >You can set Precache DRM licenses to ON in the Settings user interface to precache DRM licenses when loading content. However, best practice is to preload a specific item instead of precaching all the licenses in the catalog.
  >
  >![](assets/precache-drm-licenses.jpg)

* To use `ManagerFactory` to implement DRM error handling, make sure the following line of code is in the [!DNL PlayerFragment.java] file: 

  ```java
  drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
  
  ```

**Related API documentation**

* [Class DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html) 
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
