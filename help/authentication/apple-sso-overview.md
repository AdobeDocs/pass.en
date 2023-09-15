---
title: Apple SSO Overview
description: Apple SSO Overview
exl-id: 7cf47d01-a35a-4c85-b562-e5ebb6945693
---
# Apple SSO Overview {#apple-sso-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Introduction}

Apple provides an API which allows people to sign in to their TV provider account at the device system level, eliminating the need to authenticate on an app-by-app basis.

Hence, Apple and Adobe Pass Authentication partnered to create the platform Single Sign-On (SSO) user experience in the TV Everywhere ecosystem for iPhone, iPad and Apple TV owners.

In order to benefit from the Single Sign-On (SSO) user experience on an Apple device, there is a list of prerequisites which must be completed.

</br>

## Prerequisites {#Prerequisites}

Prerequisite may apply to one or multiple entities involved in the TVE business, such as Programmers, MVPDs, Adobe Pass Authentication or Apple.

</br>

### Programmer {#Programmer}

In order to benefit from the Single Sign-On (SSO) user experience, one Programmer must:

1.  Use at least Xcode version 8 and iOS/tvOS version 10.

1.  Have the [Video Subscriber Single Sign-On Entitlement](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) configured to their Apple Developer Account. Please contact Apple to enable [Video Subscriber Account framework](https://developer.apple.com/documentation/videosubscriberaccount) for your Apple Team ID.

1.  Enable Single Sign-On (YES) for each desired integration (Channel x MVPD) and desired platform (iOS / tvOS) through the [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/).

1.  Integrate the Apple SSO workflows using one of the following two solutions offered by Adobe Pass Authentication team:

    - The Adobe Pass Authentication REST API can support platform Single Sign-On (SSO) authentication for end users of client applications running on iOS, iPadOS or tvOS. Please see also [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

    - The Adobe Pass Authentication AccessEnabler iOS/tvOS SDK can support platform Single Sign-On (SSO) authentication for end users of client applications running on iOS, iPadOS or tvOS. Please see also [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

    - **<u>Pro Tip:</u>** In order to have access to the user's subscription information, the user must give the application permission to proceed, similar to providing access to the device's camera or microphone. This permission must be requested per application and the device will save the user's selection. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.

    - **<u>Pro Tip:</u>** We recommend requesting the user's permission when the application enters the foreground state, but it is only a suggestion, because the application can check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information at any point before requiring user authentication. Also, the AccessEnabler iOS/tvOS SDK APIs will automatically request the user's permission when needing it.

    - **<u>Pro Tip:</u>** We recommend incentivizing users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.
    
The result should create an experience in line with the following user flows, which we suggest you consult before you start developing your application/s:

- [iPhone / iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) user flows
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) user flows


>[!IMPORTANT]
>
> When the Single Sign-On feature is **enabled** for iOS/tvOS **and** in the case of Apple **onboarded (supported) or picker** MVPDs the authentication/logout flows from the Apple SSO workflows will involve both Apple and Adobe Pass Authentication solutions, while all other flows (authorization, preauthorization, metadata, etc.) will be serviced solely by Adobe Pass Authentication.


>[!IMPORTANT]
>
> When the Single Sign-On feature is **disabled** for iOS/tvOS **or** in the case of Apple **not onboarded (not supported)** MVPDs the authentication/logout flows will fallback from the Apple SSO workflows to the regular ones serviced solely by Adobe Pass Authentication.


>[!IMPORTANT]
>
> One main gain of the Apple SSO workflow is represented by the one screen authentication user flow, which can also be delivered on Apple TVs when the Single Sign-On feature is **enabled** for tvOS **and** in the case of Apple **onboarded (supported)** MVPDs.


### MVPD {#MVPD}

In order to benefit from the Single Sign-On (SSO) user experience, one
MVPD must:

 

1.  Be onboarded into the Apple SSO workflow on Apple's side. Please contact Apple to facilitate the onboarding process.
1.  Provide a JavaScript TVML application capable of handling the user login form. Please contact Apple to receive proper documentation.
1.  Provide a string value representing the provider identifier assigned by Apple during the onboarding process. Please contact Adobe Pass Authentication to perform configuration changes.

</br>

## FAQ {#FAQ}

1.  In case something goes wrong with the Apple SSO workflow, can the application using the AccessEnabler iOS/tvOS SDK have the ability to fallback to regular authentication flow?
      - This is possible but requires a configuration change being performed on the [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/). The *Enable Single Sign-On* must be set on *NO* for the desired integration (Channel x MVPD) and desired platform (iOS/tvOS).
      - The application would acknowledge the configuration change only after calling [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API in case it is using the AccessEnabler iOS/tvOS SDK.
1.  Will the application know when an authentication has happened as a result of a sign-in through the platform SSO on another device or another application?
      - This information will not be available.
1.  Will the application know when an authentication has happened as a result of a sign-in through the platform SSO on the same device? 
      - This information is available as part of the user metadata key: *tokenSource*, which should return the string value: "Apple" in this case.
1.  What happens if a user signs-in by going to the *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS section using an MVPD which is not integrated with the application?
      - When the user launches the application, the user won't be authenticated via the Apple SSO workflow. Therefore, the application would have to fallback to regular authentication flow and present its own MVPD picker.
1.  What happens if a user signs-in by going to the *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS section using an MVPD which has the *Enable Single Sign-On* set on *NO* on the [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/) for iOS/tvOS platform?
      - When the user launches the application, the user won't be authenticated via the Apple SSO workflow. Therefore, the application would have to fallback to regular authentication flow and present its own MVPD picker.
1.  What happens if a user has an MVPD which is not onboarded (not supported) by Apple, but it is present in the Apple picker?
      - When the user launches the application, the user will only select the MVPD via the Apple SSO workflow without completing the authentication flow. Therefore, the application would have to fallback to regular authentication flow, but could use the already selected MVPD.
1.  What happens if a user has an MVPD which is not onboarded (not supported) by Apple?
      - When the user launches the application, the user will select the "Other TV Providers" picker option via the Apple SSO workflow. Therefore, the application would have to fallback to regular authentication flow and present its own MVPD picker.
1.  What happens if a user has an MVPD which is degraded through the medium of [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/)?
      - When the user launches the application, the user will be authenticated via the degradation mechanism and not via the Apple SSO workflow.
      - The experience should be seamless for the user, while the application will be informed through the *N010* warning code in case it is using the AccessEnabler iOS/tvOS SDK.
1.  Will the MVPD user ID change between Apple SSO and non-Apple SSO authentication flow?
      - The expectation is that the user ID will not change, but it needs to be verified for each selected provider. 
1. Will there be any change to the authentication TTLs?
      - Adobe Pass Authentication will continue to respect the TTLs required by the Programmers for their integration with each MVPD.
      - When navigating from one Programmer application to another Programmer application through Apple SSO, the second application will have the TTL of its corresponding Programmer x MVPD integration (it won't share the TTL of the first application that authenticates)

|                                      | Adobe Pass Authentication TTL expired                                                                                      | Adobe Pass Authentication TTL valid                                                            |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple's device token TTL expired** | user is NOT authenticated (MVPD picker should appear) | user is authenticated and the TTL is the remaining time of his Adobe Pass Authentication token |
| **Apple's device token TTL valid** | user is silently authenticated and obtains another Adobe Pass Authentication token with the TTL specified in TVE Dashboard | user is authenticated and the TTL is the remaining time of his Adobe Pass Authentication token |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
