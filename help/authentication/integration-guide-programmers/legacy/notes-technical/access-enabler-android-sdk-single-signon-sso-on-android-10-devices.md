---
title: Access Enabler Android SDK Single Sign-On (SSO) on Android 10 apps
description: Access Enabler Android SDK Single Sign-On (SSO) on Android 10 apps
exl-id: dedade15-c451-4757-b684-d3728e11dd87
---
# (Legacy) Access Enabler Android SDK Single Sign-On (SSO) on Android 10 apps {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Overview

Single Sign-On (SSO) between Adobe Pass Authentication powered apps is available on devices using Android OS through the means of Access Enabler Android SDK. In order to offer Single Sign-On (SSO) on Android devices, the Access Enabler Android SDK version 3.2.1 (latest) and previous versions use a shared database file saved in an Android storage implementation, accessible by all Adobe Pass Authentication powered apps.

However, Google in latest Android 10 release produced some changes "to give users more control over their files and to limit file clutter, apps targeting Android 10 (API level 29) and higher are given scoped access into an external storage device, or scoped storage, by default. Such apps can see only their app-specific directory `\[...\]`". More details related to these Android 10 storage changes are presented in [Data and file storage documentation for Android](https://developer.android.com/training/data-storage/files/external-scoped).

As a result of these changes the Single Sign-On (SSO) offered by Access Enabler Android version **3.2.1 SDK (latest)** and previous versions can be affected on Android 10 devices as explained in the next section.

## Behavior

Depending on your app's **[!UICONTROL target SDK level]** or the usage of **android:requestLegacyExternalStorage** manifest attribute the Single Sign-On (SSO) offered by Access Enabler Android version 3.2.1 SDK (latest) and previous versions will currently behave as follows:

- Your app targets **Android 9 (API level 28)** or lower **-\>** Single Sign-On (SSO) **will work**  
- Your app targets **Android 10** **(API level 29)** and does **set** the value of **requestLegacyExternalStorage to true** in your app's manifest file **-\>** Single Sign-On (SSO) **will work**  
- Your app targets **Android 10** **(API level 29)** and does **not set** the value of **requestLegacyExternalStorage to true** in your app's manifest file **-\>** Single Sign-On (SSO) **will not work**

>[!TIP]
>
> Before Adobe Pass Authentication Access Enabler Android SDK is fully compatible with scoped storage, you can temporarily opt out based on your app's target SDK level or the requestLegacyExternalStorage manifest attribute as explained in public [Android documentation](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).
