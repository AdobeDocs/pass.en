---
title: SSO on iOS when using the Adobe Pass Authentication Access Enabler
description: SSO on iOS when using the Adobe Pass Authentication Access Enabler
exl-id: 882f0abb-2e6e-461d-a375-3ab410991935
---
# (Legacy) SSO on iOS when using the Adobe Pass Authentication Access Enabler {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

</br>

## Overview

Single Sign-On (SSO) between Adobe Pass Authentication powered apps works in different manners depending on the underlying operating system.

This document addresses **SSO on iOS**, when using the Adobe Pass Authentication **Access Enabler**.

**Access Enabler** **1.10** is the latest version of the Adobe Pass Authentication iOS native SDK. Adobe strongly recommends that you move to this version rather than staying with an older version. If you are using an older version of the Access Enabler, you can download the latest version [here](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

SSO on iOS is dictated by the following conditions:

- Apps must use the same **token storage** (in the form of a custom pasteboard that is created by the Access Enabler).
- Apps must generate the same **Device ID** (Access Enabler computes the Device ID based on the MAC address or IDFV, depending on the OS version).

## Behavior

The SSO behavior is as follows:

- **iOS 6 and lower**: SSO works automatically between apps that are developed by the same team or different teams. The Device ID is computed based on the MAC address (the same value is produced in all apps) and the storage area is common to all apps (custom pasteboard is sharable across apps on iOS 6 and lower).
    - **Important:** Please note that the iOS SDK 1.9.4 release has [increased the minimum iOS deployment target to iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7 and higher**: SSO will work in the following conditions:

1. Apps are published using the same Apple distribution profile, or profiles that belong to the same team. This is the only way for apps to share custom pasteboards on iOS 7 and upper. In all other scenarios, the pasteboard is sandboxed per application. From [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html):  \+\[`UIPasteboard pasteboardWithName:create:\`] and +\[`UIPasteboard pasteboardWithUniqueName`\] now unique the given name to allow only those apps in the same application group to access the pasteboard. If the developer attempts to create a pasteboard with a name that already exists and they are not part of the same app suite, they will get their own unique and private pasteboard. Note that this does not affect the system provided pasteboards, general, and find.

1. Apps have the same Bundle ID prefix (all components except the last). Only applications that share the same Bundle ID prefix will compute the same IDFV. From [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): On IOS 7, all components of the bundle except for the last component are used to generate the vendor ID. If the bundle ID only has a single component, then the entire bundle ID is used.

Let's now focus on the **'iOS 7 and higher'** scenario, since it's the most frequent for real users:

Both conditions (sharing a profile from the same development team and having a common bundle identifier prefix) are mandatory conditions for SSO.

Here are the possible combinations and their yielded results:

- **Profiles from the same team and the same Bundle ID prefix**: apps will share the same pasteboard storage and will have the same Device ID (IDFV). A user will need to authenticate only once (in the first app used) and the authentication state will be shared across all other apps. Example flow:

1.  User opens app A (with Bundle ID *com.x.y.AppA*) and is un-authenticated
1.  User performs authentication in app A
1.  User opens app B (with Bundle ID *com.x.y.AppB*) and is automatically authenticated by sharing the entitlement data from app
A (from step 2)
1.  User opens app A and is still authenticated (from step 2)

 

- **Profiles from the same team but different Bundle ID prefixes**: apps will share the same pasteboard storage but will have different Device IDs (IDFVs). A user will need to authenticate once per each app. Example flow:

1.  User opens app A (with Bundle ID *com.x.y.AppA*) and is un-authenticated
1.  User performs authentication in app A
1.  User opens app B (with Bundle ID *com.z.AppB*) and the Access Enabler detects the token obtained by the first app (because the storage is shared) but it will not attempt to use it via SSO because of the different Device IDs
1.  User performs authentication in app B
1.  User opens app A and is still authenticated (from step 2)

 

- **Profiles from different teams (Bundle ID is irrelevant in this scenario)**: apps will have different pasteboard storages and SSO will be disabled between them. A user will need to authenticate once per each app and the authentication sessions will remain persistent when switching between apps. Example flow:


1.  User opens app A and is un-authenticated
1.  User performs authentication in app A
1.  User opens app B and is un-authenticated
1.  User performs authentication in app B
1.  User opens app A and is authenticated (from step 2)
1.  User opens app B and is authenticated (from step 4)

**Note:** Please note that the above conditions for SSO are applicable when installing applications through the **Apple App Store**. If the apps are deployed on a simulator (where app signing doesn't apply), installed with Xcode or distributed via an Ad Hoc profile you may get different results.

**Important:** Note (**regarding AccessEnabler v1.8**): The second scenario described above (profiles from the same team but different Bundle ID prefixes) will create a very unpleasant user experience for users of the **AccessEnabler v1.8** across applications that are developed by the same team (media company). The user will be automatically logged-out when transitioning between apps from the same media company, therefore application developers must take care when deciding on the Bundle ID and distribution profile. The exact scenario in this case is presented below:

Apps will share the same pasteboard storage but will have different Device IDs (IDFVs). A user will need to authenticate once per each app, **but the authentication sessions will be erased when switching between apps**. Example flow:

1.  User opens app A (with Bundle ID *com.x.y.AppA*) and is un-authenticated
1.  User performs authentication in app A
1.  User opens app B (with Bundle ID *com.z.AppB*) and the entitlement data that was created by app A is automatically erased by the Access Enabler (security mechanism that detects a clash between the currently computed Device ID in app B and the one that is stored in the entitlement tokens - created by app A)
1.  User performs authentication in app B
1.  User opens app A and the entitlement data that was created by app B is automatically erased by the Access Enabler (security mechanism that detects a clash between the currently computed Device ID in app A and the one that is stored in the entitlement tokens - created by app B)
