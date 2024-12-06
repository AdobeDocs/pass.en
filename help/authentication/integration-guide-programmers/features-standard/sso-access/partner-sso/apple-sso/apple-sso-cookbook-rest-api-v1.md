---
title: Apple SSO Cookbook (REST API V1)
description: Apple SSO Cookbook (REST API V1)
exl-id: 072a011f-e1bb-4d3e-bcb5-697f2d1739cc
---
# Apple SSO Cookbook (REST API V1) {#apple-sso-cookbook-rest-api-v1}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The Adobe Pass Authentication REST API V1 has support for Partner Single Sign-On (SSO) for end users of client applications running on iOS, iPadOS or tvOS.

This document acts as an extension to the existing REST API V1 documentation, which can be found [here](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/rest-api-reference.md).

## Cookbook {#apple-sso-cookbook-rest-api-v1-cookbook}

In order to benefit from the Apple SSO user experience, the application needs to integrate the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) developed by Apple, while for the Adobe Pass Authentication REST API V1 communication, it needs to follow the sequence of steps presented below.

### Permission {#apple-sso-cookbook-rest-api-v1-permission}

>[!TIP]
>
> **<u>Pro Tip:</u>** The streaming application must request access to the user's subscription information saved at device level, for which the user must give the application permission to proceed, similar to providing access to the device's camera or microphone. This permission must be requested per application using Apple's [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) and the device will save the user's selection.

>[!TIP]
>
> **<u>Pro Tip:</u>** We recommend incentivizing users who refuse to give permission to access subscription information by explaining the benefits of the Apple single sign-on user experience, but be aware that the user can change their decision by going to the application settings (TV Provider permission access) or to *`Settings -> TV Provider`* on iOS and iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS.

>[!TIP]
>
> **<u>Pro Tip:</u>** We recommend requesting the user's permission when the application enters the foreground state, because the application can check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information at any point before requiring user authentication.

### Authentication {#apple-sso-cookbook-rest-api-v1-authentication}

* [Is there a valid Adobe authentication token?](#step1)
* [Is the user logged in via Partner SSO?](#step2)
* [Fetch Adobe configuration](#step3)
* [Initiate Partner SSO workflow with Adobe config](#step4)
* [Is user login successful?](#step5)
* [Obtain a profile request from Adobe for the selected MVPD](#step6)
* [Forward the Adobe request to Partner SSO to obtain the profile](#step7)
* [Exchange the Partner SSO profile for an Adobe authentication token](#step8)
* [Is Adobe token generated successfully?](#step9)
* [Initiate regular authentication workflow](#step10)
* [Proceed with authorization flows](#step11)

![](../../../../../assets/rest-api-v1/apple-sso-cookbook-rest-api-v1.png)

#### Step: "Is there a valid Adobe authentication token?" {#step1}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Check Authentication Token](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md) API service.

#### Step: "Is the user logged in via Partner SSO?" {#step2}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount).

* The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
* The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
* The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the code snippet and pay extra attention to the comments.

```swift 
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account Framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Pass Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Pass Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Partner SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Continue with the "Initiate regular authentication workflow" step.
                ...
            }
}
...  
```

#### Step: "Fetch Adobe configuration" {#step3}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Provide MVPD List](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/provide-mvpd-list.md) API service.

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the MVPD properties: *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* and pay extra attention to the comments presented in code snippets from other steps.

#### Step "Initiate Partner SSO workflow with Adobe config" {#step4}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount).

* The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
* The application would have to provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the VSAccountManager.
* The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
* The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the code snippet and pay extra attention to the comments.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account Framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Pass Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Pass Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Pass Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Pass Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Partner SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate regular authentication workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate regular authentication workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate regular authentication workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate regular authentication workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Continue with the "Initiate regular authentication workflow" step.
                    ...
                }
    }
    ...
```

#### Step: "Is user login successful?" {#step5}

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the code snippet from the ["Initiate Partner SSO workflow with Adobe config"](#step4) step. The user login is successful in case the *`vsaMetadata!.accountProviderIdentifier`* contains a valid value and the current date has not passed the *`vsaMetadata!.authenticationExpirationDate`* value.

#### Step "Obtain a profile request from Adobe for the selected MVPD" {#step6}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Profile Request](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-profilerequest.md) API service.

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware that the provider identifier obtained from the Video Subscriber Account Framework represents the *`platformMappingId`* in terms of Adobe Pass Authentication configuration. Therefore, the application must determine the MVPD id property value, using the *`platformMappingId`* value, through the medium of Adobe Pass Authentication [Provide MVPD List](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/provide-mvpd-list.md) API service.

#### Step: "Forward the Adobe request to Partner SSO to obtain the profile" {#step7}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount).


* The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
* The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
* The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the code snippet and pay extra attention to the comments.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account Framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Pass Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Pass Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Partner SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Continue with the "Initiate regular authentication workflow" step.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Continue with the "Initiate regular authentication workflow" step.
                    ...
                }
    }
    ...
```

#### Step: "Exchange the Partner SSO profile for an Adobe authentication token" {#step8}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Token Exchange](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/token-exchange.md) API service.

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the code snippet from the ["Forward the Adobe request to Partner SSO to obtain the profile"](#step7) step. This *`vsaMetadata!.samlAttributeQueryResponse!`* represents the *`SAMLResponse`*, which needs to be passed on [Token Exchange](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/token-exchange.md) and requires string manipulation and encoding (*Base64* encoded and *URL* encoded afterward) before making the call.

#### Step: "Is Adobe token generated successfully?" {#step9}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Token Exchange](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/token-exchange.md) successful response, which will be a *`204 No Content`*, indicating that the token was successfully created and is ready to be used for the authorization flows.

#### Step: "Initiate regular authentication workflow" {#step10}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Registration Code Request](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md), [Initiate Authentication](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md) and [Retrieve Authentication Token](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md) or [Check Authentication Token](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md) API services.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.

* The application would have to [obtain a registration code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) and present it to the end user on the 1st device (screen).
* The application would have to start [polling to acknowledge the authentication state](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md) on the 1st device (screen) after the registration code is obtained.
* Another application would have to [initiate authentication](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md) on a 2nd device (screen) when the registration code is used.
* The application would have to stop [polling](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md) on the 1st device (screen) when the authentication token is generated.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

* The application would have to [obtain a registration code](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md) which shouldn't be presented to the end user on the 1st device (screen).
* The application would have to [initiate authentication](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md) on the 1st device (screen) using the registration code and a [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or a [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component.
* The application would have to start [polling to knowledge the authentication state](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md) on the 1st device (screen) after the [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or the [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component closes.
* The application would have to stop [polling](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md) on the 1st device (screen) when the authentication token is generated.

#### Step: "Proceed with authorization flows" {#step11}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Initiate Authorization](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authorization.md) and [Obtain Short Media Token](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/obtain-short-media-token.md) API services.

### Logout {#apple-sso-cookbook-rest-api-v1-logout}

The [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) does not provide an API to programmatically log out people who have signed in to their TV provider account at the device system level. Therefore, for the logout to take full effect, the end user would have to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS. The other option which the user would have is to withdraw permission to access the user's subscription information from the specific application settings section (TV Provider access).

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [User Metadata Call](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md) and [Logout](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-logout.md) API services.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.

* The application would have to determine if the authentication has happened as a result of a sign-in through the partner SSO or not, using the "*tokenSource"* [user metadata](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md) from the Adobe Pass Authentication service.
* The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> Accounts -> TV Provider`* on tvOS **only** in case the *"tokenSource"* value is equal to "*Apple".*
* The application would have to [initiate the logout](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-logout.md) from the Adobe Pass Authentication service using a direct HTTP call. This would not facilitate session clean-up on the MVPD side.

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

* The application would have to determine if the authentication has happened as a result of a sign-in through the partner SSO or not, using the "*tokenSource"* [user metadata](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md) from the Adobe Pass Authentication service.
* The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS **only** in case the *"tokenSource"* value is equal to *"Apple"*.
* The application would have to [initiate the logout](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/initiate-logout.md) from the Adobe Pass Authentication service using a [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or a [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component. This would facilitate session clean-up on the MVPD side.
