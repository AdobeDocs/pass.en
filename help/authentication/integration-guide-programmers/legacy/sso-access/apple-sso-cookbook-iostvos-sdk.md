---
title: Apple SSO Cookbook (iOS/tvOS SDK)
description: Apple SSO Cookbook (iOS/tvOS SDK)
exl-id: 2d59cd33-ccfd-41a8-9697-1ace3165bc44
---
# (Legacy) Apple SSO Cookbook (iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The Adobe Pass Authentication AccessEnabler iOS/tvOS SDK has support for Partner Single Sign-On (SSO) for end users of client applications running on iOS, iPadOS or tvOS.

This document acts as an extension to the existing AccessEnabler iOS/tvOS SDK documentation, which can be found [here](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md).

## Cookbook {#apple-sso-cookbook-iostvos-sdk-cookbook}

In order to benefit from the Apple SSO user experience, the application needs to integrate the AccessEnabler iOS/tvOS SDK and follow the sequence of steps presented below.

### Prerequisites {#apple-sso-cookbook-iostvos-sdk-prerequisites}

#### Permission {#apple-sso-cookbook-iostvos-sdk-permission}

>[!TIP]
>
> **<u>Pro Tip:</u>** The streaming application must request access to the user's subscription information saved at device level, for which the user must give the application permission to proceed, similar to providing access to the device's camera or microphone. This permission must be requested per application using Apple's [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) and the device will save the user's selection.

>[!TIP]
>
> **<u>Pro Tip:</u>** We recommend incentivizing users who refuse to give permission to access subscription information by explaining the benefits of the Apple single sign-on user experience, but be aware that the user can change their decision by going to the application settings (TV Provider permission access) or to *`Settings -> TV Provider`* on iOS and iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.

>[!TIP]
>
> **<u>Pro Tip:</u>** The streaming application can request the user's permission when the application enters the foreground state, because the application can check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information at any point before requiring user authentication.

>[!TIP]
>
> **<u>Pro Tip:</u>** In case the user does not grant access to his subscription information or in case the communication with the Video Subscriber Account Framework fails, then the AccessEnabler iOS/tvOS SDK will fall back to the regular authentication flow.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

#### Callbacks {#apple-sso-cookbook-iostvos-sdk-callbacks}

>[!TIP]
>
> **<u>Pro Tip:</u>** Implement the following list of [callbacks](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md) which are specific to the Apple SSO workflow.

* [*presentTVProviderDialog*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Callback triggered when the Apple MVPD picker is going to open.
* [*dismissTVProviderDialog*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Callback triggered when the Apple MVPD picker is going to close.

#### Error Reporting {#apple-sso-cookbook-iostvos-sdk-error-reporting}

>[!TIP]
>
> **<u>Pro Tip:</u>** Implement the following list of [advanced error codes](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) which are specific to the Apple SSO workflow.

* ***N003*** - The user selected the "Other TV Provider" option from the Apple MVPD picker.
* ***N004*** - The user selected a TV Provider from the Apple MVPD picker, which is not supported (integration or Single Sign-On disabled) by the current requestor.
* ***N005*** - The user decided to cancel the regular MVPD picker or Apple MVPD picker.
* ***VSA403*** - The user's TV Provider permission is denied for the application.
* ***VSA404*** - The user's TV Provider permission is undetermined for the application.
* ***VSA503*** - The Video Subscriber Account metadata request failed, more context is provided in the *message* field.
* ***AAPL / APPL_ERROR*** - The Video Subscriber Account metadata request failed, more context is provided in the *details* field. 

### Authentication {#apple-sso-cookbook-iostvos-sdk-authentication}

>[!TIP]
>
> **<u>Tip:</u>** Follow the steps below for the iOS/iPadOS/tvOS implementation/s.

1.  The application would have to [initialise](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) the AccessEnabler iOS/tvOS SDK.


1.  The application would have to [set the current requestor identifier](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

    **Important:** This second step could trigger an [advanced error code](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    * ***VSA403*** - The user's TV Provider permission is denied for the application.
    * ***VSA404*** - The user's TV Provider permission is undetermined for the application.
    * ***APPL*** - The communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account Framework encountered an error.

    This second step would try to silently exchange the Apple SSO profile for an Adobe authentication token, in case **all of the above are false** and **all of the following are true**:

    * The user's TV Provider permission is granted for the application.
    * The user is signed in to its TV Provider account at the device system level.
    * The AccessEnabler iOS/tvOS SDK received the user's TV Provider identifier from the Video Subscriber Account Framework.
    * The user's TV Provider integration with the application is enabled through the Adobe Primetime TVE Dashboard.
    * The user's TV Provider Single Sign-On with the application is enabled through the Adobe Primetime TVE Dashboard.
    * The user's TV Provider is not degraded through the Adobe Primetime TVE Dashboard.
    * The AccessEnabler iOS/tvOS SDK received the user's TV Provider SAML response from the Video Subscriber Account Framework.

    **<u>Pro Tip:</u>** This second step will not trigger any other callbacks, besides the [setRequestorComplete](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) callback, since authentication was not explicitly initiated by the application.


1.  The application would have to [check the authentication status](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

    **Important:** This third step could trigger an [advanced error code](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    * ***VSA403** - The user is signed in to its TV Provider account at
      the device system level, but the user's TV Provider permission is
      denied for the application.
    * ***VSA404** - The user is signed in to its TV Provider account at
      the device system level, but the user's TV Provider permission
      is undetermined for the application.
    * ***APPL\_ERROR** - The user is signed in to its TV Provider
      account at the device system level, but the communication between
      the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account
      framework encountered an error.

    **Important:** This third step will trigger the [*setAuthenticationStatus*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 0, in case **one of the following is true**:

    * The user is not signed in to its TV Provider account at the device system level or through regular authentication flow.
    * The user is signed in to its TV Provider account at the device system level or through regular authentication flow, but the user's TV Provider authentication token TTL has passed.
    * The user is signed in to its TV Provider account at the device system level or through regular authentication flow, but the user's TV Provider integration with the application is disabled through the Adobe Primetime TVE Dashboard.
    * The user is signed in to its TV Provider account at the device system level, but the user's TV Provider Single Sign-On with the application is disabled through the Adobe Primetime TVE Dashboard.
    * The user is signed in to its TV Provider account at the device system level, but the user's TV Provider permission is denied for the application.
    * The user is signed in to its TV Provider account at the device system level, but the user's TV Provider permission is undetermined for the application.
    * The user is signed in to its TV Provider account at the device system level, but the communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account Framework encountered an error.

    **Important:** This third step will trigger the [*setAuthenticationStatus*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 1, in case **all of the above are false.**


1.  The application would have to [initialise the authentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) in case the previous authentication status check triggered the [*setAuthenticationStatus*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 0.

    **<u>Pro Tip:</u>** Implement one of the following AccessEnabler iOS/tvOS SDK API [getAuthentication](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN) or [getAuthentication:filter](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getAuthN_filter).

    **Important:** This fourth step could trigger an [advanced error code](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    * ***VSA403*** - The user's TV Provider permission is denied for the application.
    * ***VSA404*** - The user's TV Provider permission is undetermined for the application.
    * ***VSA503*** - The communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account Framework encountered an error.
    * ***N003*** - The user selected the "Other TV Provider" option from the Apple MVPD picker.
    * ***N004*** - The user selected a TV Provider from the Apple MVPD picker, which is not supported (integration or Single Sign-On disabled) by the current requestor.
    * ***N005*** - The user decided to cancel the regular MVPD picker or Apple MVPD picker.

    **Important:** This fourth step would fall back to the regular authentication flow, by triggering the [displayProviderDialog](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#dispProvDialog) callback and **one** of the above [advanced error codes](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md), in case **one of the above is true**. 

    **Important:** This fourth step would fall back to the regular authentication flow, by triggering the [navigateToUrl](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#nav2url) or [navigateToUrl:useSVC](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#nav2urlSVC) callback and **none** of the above [advanced error codes](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md), in case the user selected a TV provider, which does not support Apple SSO, but is present in the Apple MVPD picker.

    **<u>Pro Tip:</u>** The AccessEnabler iOS/tvOS SDK silently calls the [setSelectedPrrovder](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setSelProv) API, in case the user selected a TV provider, which does not support Apple SSO, but is present in the Apple MVPD picker.

    **Important:** This fourth step would try to silently exchange the Apple SSO profile for an Adobe authentication token, in case **all of the above are false** and **all of the following are true**:

    * The user's TV Provider permission is granted for the application.
    * The user is signed in / currently signs in to its TV Provider account at the device system level.
    * The AccessEnabler iOS/tvOS SDK received the user's TV Provider identifier from the Video Subscriber Account Framework.
    * The user's TV Provider integration with the application is enabled through the Adobe Primetime TVE Dashboard.
    * The user's TV Provider Single Sign-On with the application is enabled through the Adobe Primetime TVE Dashboard.
    * The user's TV Provider is not degraded through the Adobe Primetime TVE Dashboard.
    * The AccessEnabler iOS/tvOS SDK received the user's TV Provider SAML response from the Video Subscriber Account Framework.

    **<u>Pro Tip:</u>** This fourth step will trigger the [*setAuthenticationStatus*](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#setAuthNStatus) callback, regardless of *status* result, since authentication was explicitly initiated by the application.

### Metadata {#apple-sso-cookbook-iostvos-sdk-metadata}

The application has the option to determine if the authentication has happened as a result of a sign-in through the Partner SSO or not, using the "*tokenSource"* [user metadata](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#getMeta) API from the AccessEnabler iOS/tvOS SDK.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

### Logout {#apple-sso-cookbook-iostvos-sdk-logout}

The [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) does not provide an API to programmatically log out people who have signed in to their TV provider account at the device system level. Therefore, for the logout to take full effect, the end user would have to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS. The other option which the user would have is to withdraw permission to access the user's subscription information from the specific application settings section (TV Provider permission access).

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of AccessEnabler iOS/tvOS SDK [logout](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#logout) API.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.

* The application would have to [initiate the logout](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#logout) from the AccessEnabler iOS/tvOS SDK. This would not facilitate session clean-up on the MVPD side.
* The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> Accounts -> TV Provider`* on tvOS only in case [*VSA203* status code is triggered](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md).

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

* The application would have to [initiate the logout](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md#logout) from the AccessEnabler iOS/tvOS SDK. This would facilitate session clean-up on the MVPD side.
* The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS only in case [*VSA203* status code is triggered](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md).
