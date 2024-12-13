---
title: WKWebView support on iOS SDK 3.1+
description: WKWebView support on iOS SDK 3.1+
exl-id: 90062be0-1a0a-44ae-8d8e-f4d97a92b17a
---
# (Legacy) WKWebView support on iOS SDK 3.1+ {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

</br>

**Due to Apple deprecating UIWebView on iOS, we have updated iOS SDK 3.1 with support for WKWebView.**

## Compatibility {#compatibility}

Starting with iOS SDK version 3.1, implementors can use now WKWebView or UIWebView interchangeably. Since UIWebView is deprecated by Apple, apps should migrate to WKWebView, to avoid issues with future iOS versions.

Note that migration would imply simply switching the UIWebView class with WKWebView, there is no specific work to be done in regards to Adobe's AccessEnabler.

## Known issues {#known-issues}

Adobe's AccessEnabler used a hidden internal UIWebView instance to perform "[passive authentication](/help/authentication/integration-guide-programmers/legacy/sso-access/sso-passive-authn.md)" for certain MVPDs. The "passive" flow was useful for MVPDs that require authentication for each requestor id, and from this flow benefited those Programmers that used the same team id across multiple iOS applications in order to simulate a SSO experience (Adobe SSO). This feature is currently used by a limited number of MVPDs.

The feature used a behaviour of the UIWebView that allowed Adobe to capture the authentication cookies and replay them during the "passive" flow. WKWebView introduces stronger security that prevents Adobe to capture the cookies set at login and replay them using a hidden instance of WKWebView. Due to this security improvement and considering that the "passive" flow only benefited a very limited set of MVPDs in a very specific implementation scenario (multiple applications using same team id), Adobe removed the "passive authentication" feature for MVPDs using webviews to authenticate. 

The feature is still present for MVPDs configured to use SFSafariViewController, but note that in this case the "passive" authentication will be visible to the user since SFSafariViewController cannot be used in a "hidden" way.
