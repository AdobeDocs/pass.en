---
description: When the DRM metadata for a video is separate from the media stream, you should authenticate before you beginning the playback.
title: DRM authentication before playback
exl-id: 74eb7218-403e-4264-9063-bf959403436f
---
# DRM authentication before playback {#drm-authentication-before-playback}

When the DRM metadata for a video is separate from the media stream, you should authenticate before you beginning the playback.

A video asset can have an associated DRM metadata file, for example,:

* `"url": "https://www.domain.com/asset.m3u8"` 
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

In this example, you can use `DRMHelper` methods to download the contents of the DRM metadata file, parse it, and check whether DRM authentication is needed. 

1. Use `loadDRMMetadata` to load the metadata URL content and parse the downloaded bytes to a `DRMMetadata`.

   >[!TIP]
   >
   >This method is asynchronous and creates its own thread.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   For example:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. Notify the user that this operation is asynchronous, it is a good idea to make the user aware of that.

   If users do not know that the operation is asynchronous, they might wonder why playback has not yet started. You can, for example, show a spinner wheel while the DRM metadata is being downloaded and parsed. 

1. Implement the callbacks in the `DRMLoadMetadataListener`.

   The `loadDRMMetadata` calls these event handlers.

   ```java
   public interface DRMLoadMetadataListener { 
    
       public void onLoadMetadataUrlStart(); 
    
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   
   ```

   Here are additional details about the handlers:

    * `onLoadMetadataUrlStart` detects when the metadata URL loading has begun. 
    * `onLoadMetadataUrlComplete` detects when the metadata URL has finished loading. 
    * `onLoadMetadataUrlError` indicates that the metadata failed to load.

1. After the loading is complete, inspect the `DRMMetadata` object to determine whether DRM authentication is required.

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   For example: 

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   
   ```

1. Complete one of the following tasks:

    * If authentication is not required, begin playback. 
    * If authentication is required, complete the authentication by acquiring the license.

      ```java    
      /** 
      * Helper method to perform DRM authentication. 
      * 
      * @param drmManager 
      * the DRMManager, used to perform the authentication. 
      * @param drmMetadata 
      * the DRMMetadata, containing the DRM specific information. 
      * @param authenticationListener 
      * the listener, on which the user can be notified about the 
      * authentication process status. 
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      In this example, for simplicity, the user's name and password are explicitly coded:     
    
      ```java    
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      
      ```

1. Use an event listener to check the authentication status.

   This process implies network communication, so this is also an asynchronous operation.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   
   ```

1. If authentication is successful, start the playback.
1. If authentication is not successful, notify the user and do not start playback.

   Your application must handle any authentication errors. Failing to successfully authenticate before playing places TVSDK in an error state, and the playback stops. Your application must resolve the issue, reset the player, and reload the resource.
