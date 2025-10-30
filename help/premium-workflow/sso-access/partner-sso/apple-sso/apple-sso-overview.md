---
title: Apple SSO Overview
description: Apple SSO Overview
exl-id: 7cf47d01-a35a-4c85-b562-e5ebb6945693
---
# Apple SSO Overview {#apple-sso-overview}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Apple provides users the capability to sign in to their TV provider account at the device system level, eliminating the need to authenticate on an app-by-app basis.

Adobe Pass Authentication partnered with Apple to create the Partner Single Sign-On (SSO) user experience in the TV Everywhere ecosystem for iPhone, iPad and Apple TV owners.

In order to benefit from the Single Sign-On (SSO) user experience on an Apple device, there is a list of prerequisites documented below that must be completed.

The end result should create an experience in line with the following user flows, that we recommend you consult before you start developing your application:

* Single Sign-On (SSO) [user flows for iPhone and iPad](https://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) devices.
* Single Sign-On (SSO) [user flows for Apple TV](https://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) devices.

## Prerequisites {#apple-sso-prerequisites}

Onboarding prerequisites may apply to one or multiple entities involved in the TVE business, such as Programmers, MVPDs, Adobe Pass Authentication or Apple.

### Programmer {#apple-sso-prerequisites-programmer}

In order to benefit from the Single Sign-On (SSO) user experience, one Programmer must:

* Contact Apple to enable the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) as part of your Apple Team ID and configure the [Video Subscriber Single Sign-On Entitlement](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) as part of your Apple Developer Account.

  * Use Xcode version 8 or above and iOS/tvOS version 10 or above.

* Enable Single Sign-On (SSO) for each desired integration and platform (iOS/tvOS) through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) by setting the `Enable Single Sign On` property to `Yes`.

| Adobe Enable Single Sign On | Apple **Onboarded (Supported)** MVPDs                                                                                                                                                                                              | Apple **Picker** MVPDs                                                                                               | Apple **Not Onboarded (Not Supported)** MVPDs                                                                        |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Yes (Enabled)               | The authentication and logout flows will involve both Apple and Adobe Pass Authentication solutions, while all other flows (authorization, preauthorization, metadata, etc.) will be serviced solely by Adobe Pass Authentication. | The authentication and logout flows will fall back to the regular ones serviced solely by Adobe Pass Authentication. | The authentication and logout flows will fall back to the regular ones serviced solely by Adobe Pass Authentication. |
| No (Disabled)               | The authentication and logout flows will fall back to the regular ones serviced solely by Adobe Pass Authentication.                                                                                                               | The authentication and logout flows will fall back to the regular ones serviced solely by Adobe Pass Authentication. | The authentication and logout flows will fall back to the regular ones serviced solely by Adobe Pass Authentication. |

* Integrate the Single Sign-On (SSO) user flows using one of the following solutions offered by Adobe Pass Authentication for end users of client applications running on iOS, iPadOS or tvOS.

  * The Adobe Pass Authentication REST API V2 has support for Partner Single Sign-On (SSO).

    Refer to the [Apple SSO Cookbook (REST API V2)](apple-sso-cookbook-rest-api-v2.md) documentation.

  * The legacy Adobe Pass Authentication REST API V1 has support for Partner Single Sign-On (SSO).

    Refer to the [(Legacy) Apple SSO Cookbook (REST API V1)](/help/authentication/integration-guide-programmers/legacy/sso-access/apple-sso-cookbook-rest-api-v1.md) documentation.

  * The legacy Adobe Pass Authentication AccessEnabler iOS/tvOS SDK has support for Partner Single Sign-On (SSO).

    Refer to the [(Legacy) Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/integration-guide-programmers/legacy/sso-access/apple-sso-cookbook-iostvos-sdk.md) documentation.

### MVPD {#apple-sso-prerequisites-mvpd}

In order to benefit from the Single Sign-On (SSO) user experience, one MVPD must:

* Contact Apple to initiate the onboarding process on Apple's side.

  * Request the technical documentation on how to integrate and develop a JavaScript TVML application capable of handling the user login form.

* Contact Adobe Pass Authentication to initiate the onboarding process on Adobe's side.

  * Provide the string value representing the TV provider identifier assigned by Apple during the onboarding process.

## FAQ {#FAQ}

* In case something goes wrong with the Apple SSO workflow, can the application using the Adobe Pass Authentication AccessEnabler iOS/tvOS SDK have the ability to fall back to the regular authentication flow?

  This is possible but requires a configuration change being performed through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) to set the **Enable Single Sign-On** on **NO** for the desired integration and platform (iOS/tvOS). Be aware that the client application will acknowledge the configuration change only after calling the [setRequestor](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setReqV3) API.


* Will the application know when an authentication has happened as a result of a sign in through Apple SSO?

  This information is available as part of the user metadata key: *tokenSource*, which should return the string value: "Apple" in this case.


* Will the application know when an authentication has happened as a result of a sign in through Apple SSO on another application?

  This information is not available.


* What happens if a user signs in by going to the *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS section using an MVPD which is not integrated with the application?

  When the user launches the application, the user won't be authenticated via the Apple SSO workflow. Therefore, the application would have to fall back to regular authentication flow and present its own MVPD picker.

 
* What happens if a user signs in by going to the *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS section using an MVPD which has the **Enable Single Sign On** set on **NO** through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) for iOS/tvOS platform?

  When the user launches the application, the user won't be authenticated via the Apple SSO workflow. Therefore, the application would have to fall back to regular authentication flow and present its own MVPD picker.

 
* What happens if a user has an MVPD which is not onboarded (not supported) by Apple, but it is present in the Apple picker?

  When the user launches the application, the user will only select the MVPD via the Apple SSO workflow without completing the authentication flow. Therefore, the application would have to fall back to regular authentication flow, but could use the already selected MVPD.

 
* What happens if a user has an MVPD which is not onboarded (not supported) by Apple?

  When the user launches the application, the user will select the "Other TV Providers" picker option via the Apple SSO workflow. Therefore, the application would have to fall back to regular authentication flow and present its own MVPD picker.

 
* What happens if a user has an MVPD which is degraded through the medium of [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication)?

  When the user launches the application, the user will be authenticated via the degradation mechanism and not via the Apple SSO workflow. The experience should be seamless for the user, while the application will be informed through the *N010* warning code in case it is using the Adobe Pass Authentication AccessEnabler iOS/tvOS SDK.


* Will the MVPD user ID change between Apple SSO and non-Apple SSO authentication flows?

  The expectation is that the user ID will not change, but it needs to be verified for each selected provider.


* Will there be any change to the authentication TTLs?

  Adobe Pass Authentication will continue to respect the TTLs required by the Programmers for their integration with each MVPD. When navigating from one Programmer application to another Programmer application through Apple SSO, the second application will have the TTL of its corresponding Programmer x MVPD integration (it won't share the TTL of the first application that authenticates)

|                                      | Adobe Pass Authentication TTL expired                                                                                              | Adobe Pass Authentication TTL valid                                                                    |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Apple's device token TTL expired** | user is NOT authenticated (MVPD picker should appear)                                                                              | user is authenticated and the TTL is the remaining time of his Adobe Pass Authentication token/profile |
| **Apple's device token TTL valid**   | user is silently authenticated and obtains another Adobe Pass Authentication token/profile with the TTL specified in TVE Dashboard | user is authenticated and the TTL is the remaining time of his Adobe Pass Authentication token/profile |
