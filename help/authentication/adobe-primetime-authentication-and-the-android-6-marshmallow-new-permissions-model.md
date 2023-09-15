---
title: Adobe Pass Authentication and the Android 6 "Marshmallow" New Permissions Model
description: Adobe Pass Authentication and the Android 6 "Marshmallow" New Permissions Model
exl-id: 3c96769e-b25b-48ab-bb74-40f13d4e5a84
---
# Adobe Pass Authentication and the Android 6 "Marshmallow" New Permissions Model {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

The new Android 6 Marshmallow release introduces some updates to the permissions model, which can affect the behavior of apps that use the existing Adobe Pass authentication SDK version 1.8 and older. 

As a new feature, the new Android OS offers [granular control over the permissions that apps require at the time of installation and at runtime](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>The changes described below will **only affect applications developed specifically for Android 6.0** (targetSdkVersion=23). They do not affect older applications already installed on the user's device when upgrading to Android 6.0. 


Specifically, for apps developed in Android Studio using [API level 23](http://developer.android.com/sdk/api_diff/23/changes.html) and which use the Adobe Pass Authentication SDK, the developer will need to write custom code (see code snippet below) [to trigger the allow/deny permissions dialogue](https://developer.android.com/training/permissions/requesting.html). 

Following is the code excerpt used for requesting write access to the device external storage:

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**From the users' perspective**, upon installation, users are greeted by a window prompting them to confirm read/write permissions for files (see figure 2 below). This leads to one of the following two outcomes:

1.  If the user **confirms** the permissions, the regular authentication flow will be kept and tokens will be stored in the global storage. Users will stay authenticated in the app and across apps using Adobe Pass authentication for as long as the tokens are valid.
1.  If the user **denies** the permissions, write actions in the storage will fail and the users will only be authenticated until they exit the app. Please note that some applications reinitialize when switching between foreground and background, so that the users will be logged out when performing this action. Tokens are NOT stored and the users will need to authenticate every time they use the app. 


>[!TIP]
>
>A feature which introduces storage resilience is currently in development for the Adobe Pass authentication SDK 1.9. The new SDK is targeted for **release in the last week of October**. The application will fallback to writing in the application's sandbox storage whenever the general storage cannot be used. This covers the case in which, for applications developed in API level 23, users do NOT accept read/write permissions in the global storage. The tokens are stored individually per app which means that Single-Sign-On between apps using Adobe Pass authentication will be disabled.


![](assets/android-permissions-request.png)

*Figure: The permission request dialogue for apps written targeting API level 23*

>[!IMPORTANT]
>
> Adobe advises **its partners to develop apps using API level 22 (targetSdkVersion=22) or older in order to guarantee the best possible user experience in the authentication process**.
