---
title: Apple SSO Cookbook (iOS/tvOS SDK)
description: Apple SSO Cookbook (iOS/tvOS SDK)
exl-id: 2d59cd33-ccfd-41a8-9697-1ace3165bc44
---
# Apple SSO Cookbook (iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Introduction}

The Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK can support platform Single Sign-On (SSO) authentication for end users of client applications running on iOS, iPadOS or tvOS through what we call Apple SSO workflow.

Please note that this document acts as an extension to the existing AccessEnabler iOS/tvOS SDK documentation, which can be found [here](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## Cookbook {#Cookbook}

In order to benefit from the Apple SSO user experience, one application would need to integrate the AccessEnabler iOS/tvOS SDK and follow the sequence of tips presented below.

</br>

### Prerequisites {#Prerequisites}

</br>

#### Permission

>[!TIP]
>
> **<u>Pro Tip:</u>** In order to have access to the user's subscription information, the user must give the application permission to proceed, similar to providing access to the device's camera or microphone. This permission must be requested per application and the device will save the user's selection. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.

>[!TIP]
>
> **<u>Pro Tip:</u>** We recommend requesting the user's permission when the application enters the foreground state, but it is only a suggestion, because the application can check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information at any point before requiring user authentication. Also, the AccessEnabler iOS/tvOS SDK APIs will automatically request the user's permission when needing it.

>[!TIP]
>
> **<u>Pro Tip:</u>** In case the user does not grant access to his subscription information or in case the communication with the Video Subscriber Account framework fails, then the AccessEnabler iOS/tvOS SDK will fallback to the regular authentication flow.

>[!TIP]
>
> **<u>Pro Tip:</u>** We recommend incentivizing users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.


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

</br>

#### Callbacks

>[!TIP]
>
> **<u>Pro Tip:</u>** Implement the following list of [callbacks](/help/authentication/iostvos-sdk-api-reference.md) which are specific to the Apple SSO workflow.

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Callback triggered when the Apple MVPD picker is going to open.
- [*dismissTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Callback triggered when the Apple MVPD picker is going to close.

</br>

#### Error Reporting

>[!TIP]
>
> **<u>Pro Tip:</u>** Implement the following list of [advanced error codes](/help/authentication/error-reporting.md) which are specific to the Apple SSO workflow.

- ***N003*** - The user selected the "Other TV Provider" option from the Apple MVPD picker.
- ***N004*** - The user selected a TV Provider from the Apple MVPD picker, which is not supported (integration or Single Sign-On disabled) by the current requestor.
- ***N005*** - The user decided to cancel the regular MVPD picker or Apple MVPD picker.
- ***VSA403*** - The user's TV Provider permission is denied for the application.
- ***VSA404*** - The user's TV Provider permission is undetermined for the application.
- ***VSA503*** - The Video Subscriber Account metadata request failed, more context is provided in the *message* field.
- ***AAPL / APPL_ERROR*** - The Video Subscriber Account metadata request failed, more context is provided in the *details* field. 

</br>

### Authentication {#Authentication}

>[!TIP]
>
> **<u>Tip:</u>** Follow the steps below for the iOS/iPadOS/tvOS implementation/s.

1.  The application would have to [initialise](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) the AccessEnabler iOS/tvOS SDK.
1.  The application would have to [set the current requestor identifier](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

    **Important:** This second step could trigger an [advanced error code](/help/authentication/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    - ***VSA403*** - The user's TV Provider permission is denied for the application.
    - ***VSA404*** - The user's TV Provider permission is undetermined for the application.
    - ***APPL*** - The communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account framework encountered an error.

    This second step would try to silently exchange the Apple SSO profile for an Adobe authentication token, in case **all of the above are false** and **all of the following are true**:

    - The user's TV Provider permission is granted for the application.
    - The user is signed in to its TV Provider account at the device system level.
    - The AccessEnabler iOS/tvOS SDK received the user's TV Provider identifier from the Video Subscriber Account framework.
    - The user's TV Provider integration with the application is enabled through the Adobe Primetime TVE Dashboard.
    - The user's TV Provider Single Sign-On with the application is enabled through the Adobe Primetime TVE Dashboard.
    - The user's TV Provider is not degraded through the Adobe Primetime TVE Dashboard.
    - The AccessEnabler iOS/tvOS SDK received the user's TV Provider SAML response from the Video Subscriber Account framework.

    **<u>Pro Tip:</u>** This second step will not trigger any other callbacks, besides the [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) callback, since authentication was not explicitly initiated by the application.

1.  The application would have to [check the authentication status](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

    **Important:** This third step could trigger an [advanced error code](/help/authentication/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    - ***VSA403** - The user is signed in to its TV Provider account at
      the device system level, but the user's TV Provider permission is
      denied for the application.
    - ***VSA404** - The user is signed in to its TV Provider account at
      the device system level, but the user's TV Provider permission
      is undetermined for the application.
    - ***APPL\_ERROR** - The user is signed in to its TV Provider
      account at the device system level, but the communication between
      the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account
      framework encountered an error.

    **Important:** This third step will trigger the [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 0, in case **one of the following is true**:

    - The user is not signed in to its TV Provider account at the device system level or through regular authentication flow.
    - The user is signed in to its TV Provider account at the device system level or through regular authentication flow, but the user's TV Provider authentication token TTL has passed.
    - The user is signed in to its TV Provider account at the device system level or through regular authentication flow, but the user's TV Provider integration with the application is disabled through the Adobe Primetime TVE Dashboard.
    - The user is signed in to its TV Provider account at the device system level, but the user's TV Provider Single Sign-On with the application is disabled through the Adobe Primetime TVE Dashboard.
    - The user is signed in to its TV Provider account at the device system level, but the user's TV Provider permission is denied for the application.
    - The user is signed in to its TV Provider account at the device system level, but the user's TV Provider permission is undetermined for the application.
    - The user is signed in to its TV Provider account at the device system level, but the communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account framework encountered an error.

    **Important:** This third step will trigger the [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 1, in case **all of the above are false.**


1.  The application would have to [initialise the authentication](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) in case the previous authentication status check triggered the [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback with *status* equal to 0.

    **<u>Pro Tip:</u>** Implement one of the following AccessEnabler iOS/tvOS SDK API [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) or [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

      **Important:** This fourth step could trigger an [advanced error code](/help/authentication/error-reporting.md) which is specific to the Apple SSO workflow, in case **one of the following is true**:

    - ***VSA403*** - The user's TV Provider permission is denied for the application.
    - ***VSA404*** - The user's TV Provider permission is undetermined for the application.
    - ***VSA503*** - The communication between the AccessEnabler iOS/tvOS SDK and the Video Subscriber Account framework encountered an error.
    - ***N003*** - The user selected the "Other TV Provider" option from the Apple MVPD picker.
    - ***N004*** - The user selected a TV Provider from the Apple MVPD picker, which is not supported (integration or Single Sign-On disabled) by the current requestor.
    - ***N005*** - The user decided to cancel the regular MVPD picker or Apple MVPD picker.

    **Important:** This fourth step would fallback to the regular authentication flow, by triggering the [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) callback and **one** of the above [advanced error codes](/help/authentication/error-reporting.md), in case **one of the above is true**. 

    **Important:** This fourth step would fallback to the regular authentication flow, by triggering the [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) or [navigateToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) callback and **none** of the above [advanced error codes](/help/authentication/error-reporting.md), in case the user selected a TV provider, which does not support Apple SSO, but is present in the Apple MVPD picker.

    **<u>Pro Tip:</u>** The AccessEnabler iOS/tvOS SDK silently calls the [setSelectedPrrovder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API, in case the user selected a TV provider, which does not support Apple SSO, but is present in the Apple MVPD picker.

    **Important:** This fourth step would try to silently exchange the Apple SSO profile for an Adobe authentication token, in case **all of the above are false** and **all of the following are true**:

    - The user's TV Provider permission is granted for the application.
    - The user is signed in / currently signs in to its TV Provider account at the device system level.
    - The AccessEnabler iOS/tvOS SDK received the user's TV Provider identifier from the Video Subscriber Account framework.
    - The user's TV Provider integration with the application is enabled through the Adobe Primetime TVE Dashboard.
    - The user's TV Provider Single Sign-On with the application is enabled through the Adobe Primetime TVE Dashboard.
    - The user's TV Provider is not degraded through the Adobe Primetime TVE Dashboard.
    - The AccessEnabler iOS/tvOS SDK received the user's TV Provider SAML response from the Video Subscriber Account framework.

 

>**<u>Pro Tip:</u>** This fourth step will trigger the [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) callback, regardless of *status* result, since authentication was explicitly initiated by the application.


</br>

### Metadata {#Metadata}

The application has the option to determine if the authentication has happened as a result of a sign-in through the platform SSO or not, using the "*tokenSource"* [user metadata](/help/authentication/iostvos-sdk-api-reference.md#getMeta) API from the AccessEnabler iOS/tvOS SDK.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### Logout {#Logout}

The [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework does not provide an API to programatically log out people who have signed in to their TV provider account at the device system level. Therefore, for the logout to take full effect, the end user would have to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS. The other option which the user would have is to withdraw permission to access the user's subscription information from the specific application settings section (TV Provider permission access).

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of AccessEnabler iOS/tvOS SDK [logout](/help/authentication/iostvos-sdk-api-reference.md#logout) API.


>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.

- The application would have to [initiate the logout](/help/authentication/iostvos-sdk-api-reference.md#logout) from the AccessEnabler iOS/tvOS SDK. This would not facilitate session clean-up on the MVPD side.
- The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> Accounts -> TV Provider`* on tvOS only in case [*VSA203* status code is triggered](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

- The application would have to [initiate the logout](/help/authentication/iostvos-sdk-api-reference.md#logout) from the AccessEnabler iOS/tvOS SDK. This would facilitate session clean-up on the MVPD side.
- The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS only in case [*VSA203* status code is triggered](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
