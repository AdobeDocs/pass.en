---
description: When the DRM metadata for a video is separate from the media stream, perform authentication before beginning playback.
title: DRM authentication before playback
exl-id: da81ec38-ea77-4fcd-a6e4-5804465385cb
---
# DRM authentication before playback {#drm-authentication-before-playback}

When the DRM metadata for a video is separate from the media stream, perform authentication before beginning playback.

A video asset can have an associated DRM metadata file. For example:

* "url": "ht<span></span>tps://www.domain.com/asset.m3u8" 
* "drmMetadata": "ht<span></span>tps://www.domain.com/asset.metadata"

When this is the case, use `DRMHelper` methods to download the contents of the DRM metadata file, parse it, and check whether DRM authentication is needed. 

1. Use `loadDRMMetadata` to load the metadata URL content and parse the downloaded bytes to a `DRMMetadata`.

   Like any other network operation, this method is asynchronous, creating its own thread.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   For example:

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. Because the operation is asynchronous, it is a good idea to make the user aware of that. Otherwise, he'll wonder why his playback is not beginning. For example, show a spinner wheel while the DRM metadata is being downloaded and parsed.
1. Implement the callbacks in the `DRMLoadMetadataListener`. The `loadDRMMetadata` calls these event handlers (dispatches these events).

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

    * `onLoadMetadataUrlStart` detects when the metadata URL loading has begun. 
    * `onLoadMetadataUrlComplete` detects when the metadata URL has finished loading. 
    * `onLoadMetadataUrlError` indicates that the metadata failed to load.

1. When loading completes, inspect the `DRMMetadata` object to see whether DRM authentication is needed.

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. If authentication is not needed, begin playback.
1. If authentication is needed, perform the authentication by acquiring the license.

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

   This example, for simplicity, explicitly codes the user's name and password.

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   
   ```

1. This also implies network communication, hence this is also an asynchronous operation. Use an event listener to check the authentication status.

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   
   ```

1. If authentication is successful, start playback.
1. If authentication is not successful, notify the user and do not start playback.

Your application must handle any authentication errors. Failing to successfully authenticate before playing places TVSDK into an error state. That is, it changes its state to ERROR, an error is generated containing the error code from the DRM library, and the playback stops. Your application must resolve the issue, reset the player, and reload the resource.
