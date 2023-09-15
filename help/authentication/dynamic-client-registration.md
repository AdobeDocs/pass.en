---
title: Dynamic Client Registration
description: Dynamic Client Registration
exl-id: 9bc2597d-b634-4542-849b-8e91a76cb8da
---
# Dynamic Client Registration {#dynamic-client-registration}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Context {#context}

To align with modern security practices, improved UX and platform owners
requirements, Adobe Pass Authentication Android SDK and iOS SDK are moving in the direction of adopting [Android Chrome custom tabs](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

The current AdobePass implementation uses platform specific web views, in order to provide the web environment for displaying the MVPD login page. These web views do not share credential management with platform browsers, thus the user cannot use a browser saved password when using an Adobe Pass Authentication application. Moreover, for security reasons, some platforms are moving to deprecate the WebView controllers for authentication tasks. Both Google and Apple provide alternate options such as "Chrome Custom Tabs" and "Safari View Controller". These are basically single use tabs of their respective browsers. Adobe Pass Authentication will adopt these new components in 2018.

## Details {#details}

Currently, there are two ways in which Adobe Pass Authentication identifies and registers applications:

* browser-based clients are registered via allowed domain listing
* native application clients, such as iOS and Android applications are registered through signed requestor mechanism

In order to address the new flows for Chrome Custom Tabs & Safari View Controller, Adobe Pass proposes a new client registration mechanism for registering new applications. This mechanism will allow a more secure and granular control of your applications and it can be used to register applications on all platforms.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
