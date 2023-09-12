---
title: License acquisition process details
description: License acquisition process details
copied-description: yes
exl-id: d772339a-8d05-401b-b5c1-18169b3627b6
---
# License acquisition process details {#license-acquisition-process-details}

This process presents a detailed, API-level view of the Primetime DRM protected-content workflow: 

1. Using a `URLLoader` object, load the bytes of the protected content's metadata file.

   Set this object to a variable, such as `metadata_bytes`. All content controlled by Primetime DRM has Primetime DRM metadata. When the content is packaged, this metadata can be saved as a separate metadata file ( [!DNL .metadata]) alongside the content. Alternatively, the metadata can be Base64-encoded and inserted into the body of the video manifest file. For more information, see [Packaging Media Files](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. If necessary, remove the exclamation point `!` from the start of the string.
   1. If necessary for HLS or HDS content, decode the included metadata in the Base64-encoded string to binary data before passing it.
1. Create a `DRMContentData` instance.

   Put this code into a try-catch block: 

   ```
   new DRMContentData(metadata_bytes)
   ```

   where `metadata_bytes` is the `URLLoader` object obtained in Step 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Create listeners to listen for the `DRMStatusEvent` and `DRMErrorEvent` dispatched from the `DRMManager` object.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   In the `DRMStatusEvent` listener, check that the license is valid (not null). In the `DRMErrorEvent` listener, handle `DRMErrorEvents`. See *Using the DRMStatusEvent class* and *Using the DRMErrorEvent class* in this guide.

1. Load the license that is required to play the content.
   First, try to load a locally stored license to play the content: 

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   After loading completes, the `DRMManager` object dispatches `DRMStatusEvent.DRM_Status`. 
   
1. Check the `DRMVoucher` object.


   If the `DRMVoucher` object is not null, the license is valid. Go to Step 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Check the authentication method required by the policy for this content.

   Use the `DRMContentData.authenticationMethod` property.
   1. If the authentication method is `ANONYMOUS`, go to Step 9. 
   
      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)   
   
      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)   
   1. If the authentication method is `USERNAME_AND_PASSWORD`, your application must provide a mechanism to let the user enter credentials.
   
      Pass the user's credentials to the license server to authenticate the user:    
   
      ```   
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```   
   
      The `DRMManager` dispatches a `DRMAuthenticationErrorEvent` if authentication fails, or a `DRMAuthenticationCompleteEvent` if authentication succeeds. Create listeners for these events.   
   
      [Android: authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))   
   
      [iOS: authenticate:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe recommends using a more secure mechanism to provide credentials. For reference, see the [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. If the authentication method is `UNKNOWN`, you must use a custom authentication method.
   
      In this case, the content provider has arranged for authentication to be done in an out-of-band manner, not using the Primetime APIs. The custom authentication procedure must produce an authentication token that can be passed to the `DRMManager.setAuthenticationToken()` method.   
   
      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))   
   
      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Alternatively, regardless of the authentication method, `.setAuthenticationToken()` can be used to send custom data from the client to the license server. This is an overloading of the API, as this mechanism is the only way to send dynamic custom data from the client to the license server at the time of license acquisition. This method of custom data transport is discussed in depth in several forum posts in the [Primetime DRM (Adobe Access) forums ](https://forums.adobe.com/community/adobe_access).

1. If authentication fails, your application must return to Step 6.

   Ensure that your application has a mechanism to handle and limit repeated authentication failures. For example, after three attempts, you display a message to the user indicating the authentication has failed and content cannot be played.
1. To use the stored token instead of prompting the user to enter credentials, set the token with the `DRMManager.setAuthenticationToken()` method.

   You then download the license from the license server and play content as in Step 6.
   1. **Optional:** If authentication succeeds, you can capture the authentication token, which is a byte array cached in memory.
   
      Get this token with the `DRMAuthenticationCompleteEvent.token` property. You can store and use the authentication token so that the user does not have to repeatedly enter credentials for this content. The license server determines the valid period of the authentication token.   
   
      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)   
   
      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)   
1. If authentication succeeds, download the license from the license server:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   After loading completes, the `DRMManager` object dispatches `DRMStatusEvent.DRM_STATUS`. Listen for this event, and when it is dispatched, you can play the content.  Play the video by creating a Primetime object and then calling its `play()` method: 

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android: acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)
