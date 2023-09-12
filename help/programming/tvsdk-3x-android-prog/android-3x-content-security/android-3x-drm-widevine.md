---
description: You can use the features of the Primetime Digital Rights Management (DRM) system to provide secure access to your video content. Alternatively, you can use third-party DRM solutions as an alternative to Adobe's integrated solution.
title: Widevine DRM
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
---
# Widevine DRM {#widevine-drm}

You can use the features of the Primetime Digital Rights Management (DRM) system to provide secure access to your video content. Alternatively, you can use third-party DRM solutions as an alternative to Adobe's integrated solution.

Contact your Adobe representative for the most up-to-date information on the availability of third-party DRM solutions.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

You can use the Android native Widevine DRM with HLS CMAF streams.

>[!NOTE]
>
> Widevine CENC CTR Scheme requires minimum Android version 4.4 (API Level 19).
>
> Widevine CBCS Scheme requires minimum Android version 7.1 (API Level 25).

## Set license server details {#license-server-details}

Call the following `com.adobe.mediacore.drm.DRMManager` API before loading MediaPlayer resource:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Arguments {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` for Widevine.

* `licenseServerURL` - The URL of the Widevine license server that receives license requests.

* `requestProperties` - Contains extra headers to include in the outgoing license request.

For example, when using content packaged for Expressplay DRM, use the following code before playing:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Provide custom callback {#custom-callback}

Call the following `com.adobe.mediacore.drm.DRMManager` API before loading MediaPlayer resource.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Arguments {#arguments-custom-callback}

* `callback` - custom implementation of MediaDrmCallback to use instead of the default `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

For details, see [Android TVSDK 3.11 API documentation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Fetch PSSH Box of current loaded MediaPlayer resource {#pssh-box-mediaplayer-resoource}

Call the following `com.adobe.mediacore.drm.DRMManager` API, preferably in custom callback implementation.

```java
public static byte[] getPSSH()
```

API returns the Protection System Specific Header Box associated with the loaded Widevine media resource.

A valid box is available for short duration (between DRM instance creation and loading of keys). `MediaDrmCallback callback executeKeyRequest()` can use it to customize fetching license keys.

>[!NOTE]
>
> `getPSSH()` API is supported with single player instance only. Multiple players or Instant On feature should initialize serially to receive the correct box.
