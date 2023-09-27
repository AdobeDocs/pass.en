---
title: Apple SSO Cookbook (REST API)
description: Apple SSO Cookbook (REST API)
exl-id: cb27c4b7-bdb4-44a3-8f84-c522a953426f
---
# Apple SSO Cookbook (REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Introduction}

The Adobe Pass Authentication REST API can support platform Single Sign-On (SSO) authentication for end users of client applications running on iOS, iPadOS or tvOS through what we call Apple SSO workflow.

Please note that this document acts as an extension to the existing REST API documentation, which can be found [here](/help/authentication/rest-api-reference.md).

## Cookbooks {#Cookbooks}

In order to benefit from the Apple SSO user experience, one application would need to integrate the [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework developed by Apple, while regarding the Adobe Pass Authentication REST API communication, it would have to follow the sequence of tips presented below.

### Authentication {#Authentication}

- [Is there a valid Adobe authentication token?](#Is_there_a_valid_Adobe_authentication_token)
- [Is the user logged in via Platform SSO?](#Is_the_user_logged_in_via_Platform_SSO)
- [Fetch Adobe configuration](#Fetch_Adobe_configuration)
- [Initiate Platform SSO workflow with Adobe config](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [Is user login successful?](#Is_user_login_successful)
- [Obtain a profile request from Adobe for the selected MVPD](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [Forward the Adobe request to Platform SSO to obtain the profile](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [Exchange the Platform SSO profile for an Adobe authentication token](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [Is Adobe token generated successfully?](#Is_Adobe_token_generated_successfully)
- [Initiate second screen authentication workflow](#Initiate_second_screen_authentication_workflow)
- [Proceed with authorization flows](#Proceed_with_authorization_flows)

 
![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)


#### Step: "Is there a valid Adobe authentication token?" {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Adobe Pass Authentication](/help/authentication/check-authentication-token.md) service.


#### Step: "Is the user logged in via Platform SSO?" {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework.

- The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
- The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
- The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

 

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
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
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
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

#### Step: "Fetch Adobe configuration" {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Adobe Pass Authentication](/help/authentication/provide-mvpd-list.md) service.


>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the MVPD properties: *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* and pay extra attention to the comments presented in code snippets from other steps.

#### Step "Initiate Platform SSO workflow with Adobe config" {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework.

- The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
- The application would have to provide a [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) for the VSAccountManager.
- The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
- The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

 

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
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
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
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
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
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Step: "Is user login successful?" {#Is_user_login_successful}

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the code snippet from the ["Initiate Platform SSO workflow with Adobe config"](#Initiate_Platform_SSO_workflow_with_Adobe_config) step. The user login is successful in case the *`vsaMetadata!.accountProviderIdentifier`* contains a valid value and the current date has not passed the *`vsaMetadata!.authenticationExpirationDate`* value.

#### Step "Obtain a profile request from Adobe for the selected MVPD" {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Profile Request](/help/authentication/retrieve-profilerequest.md) service.

>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware that the provider identifier obtained from the Video Subscriber Account framework represents the *`platformMappingId`* in terms of Adobe Pass Authentication configuration. Therefore, the application must determine the MVPD id property value, using the *`platformMappingId`* value, through the medium of Adobe Pass Authentication [Provide MVPD List](/help/authentication/provide-mvpd-list.md) service.

#### Step: "Forward the Adobe request to Platform SSO to obtain the profile" {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework.


- The application would have to check for [permission to access](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) the user's subscription information and proceed only if the user allowed it.
- The application would have to submit a [request](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) for subscriber account information.
- The application would have to wait and process the [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) information.

 

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
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
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
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Step: "Exchange the Platform SSO profile for an Adobe authentication token" {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Token Exchange](/help/authentication/token-exchange.md) service.


>[!TIP]
>
> **<u>Pro Tip:</u>** Please be aware of the code snippet from the ["Forward the Adobe request to Platform SSO to obtain the profile"](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) step. This *`vsaMetadata!.samlAttributeQueryResponse!`* represents the *`SAMLResponse`*, which needs to be passed on [Token Exchange](/help/authentication/token-exchange.md) and requires string manipulation and encoding (*Base64* encoded and *URL* encoded afterwards) before making the call.

</br>

#### Step: "Is Adobe token generated successfully?" {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium Adobe Pass Authentication [Token Exchange](/help/authentication/token-exchange.md) successful response, which will be a *`204 No Content`*, indicating that the token was successfully created and is ready to be used for the authorization flows.

</br>

#### Step: "Initiate second screen authentication workflow" {#Initiate_second_screen_authentication_workflow}

**Important:** "Second screen authentication workflow" terminology is appropriate for AppleTVs, while "First screen authentication workflow" / "Regular authentication workflow" terminology would be more appropriate for iPhones and iPads.


>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication

[Registration Code Request](/help/authentication/registration-code-request.md), [Initiate Authentication](/help/authentication/initiate-authentication.md) and [REST API Retrieve Authentication Token](/help/authentication/retrieve-authentication-token.md) or [Check Authentication Token](/help/authentication/check-authentication-token.md) services.


>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.

- The application would have to [obtain a registration code](/help/authentication/registration-code-request.md) and present it to the end user on the 1st device (screen).
- The application would have to start [polling to acknowledge the authentication state](/help/authentication/retrieve-authentication-token.md) on the 1st device (screen) after the registration code is obtained.
- Another application would have to [initiate authentication](/help/authentication/initiate-authentication.md) on a 2nd device (screen) when the registration code is used.
- The application would have to stop [polling](/help/authentication/retrieve-authentication-token.md) on the 1st device (screen) when the authentication token is generated.

 

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

- The application would have to [obtain a registration code](/help/authentication/registration-code-request.md) which shouldn't be presented to the end user on the 1st device (screen).
- The application would have to [initiate authentication](/help/authentication/initiate-authentication.md) on the 1st device (screen) using the registration code and a [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or a [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component.
- The application would have to start [polling to knowledge the authentication state](/help/authentication/retrieve-authentication-token.md) on the 1st device (screen) after the [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or the [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component closes.
- The application would have to stop [polling](/help/authentication/retrieve-authentication-token.md) on the 1st device (screen) when the authentication token is generated.

</br>

#### Step: "Proceed with authorization flows" {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [Initiate Authorization](/help/authentication/initiate-authorization.md) and [Obtain Short Media Token](/help/authentication/obtain-short-media-token.md) services.

</br>

### Logout {#Logout}

The [Video Subscriber Account](https://developer.apple.com/documentation/videosubscriberaccount) framework does not provide an API to programatically log out people who have signed in to their TV provider account at the device system level. Therefore, for the logout to take full effect, the end user would have to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS or *`Settings -> Accounts -> TV Provider`* on tvOS. The other option which the user would have is to withdraw permission to access the user's subscription information from the specific application settings section (TV Provider access).

>[!TIP]
>
> **<u>Tip:</u>** Implement this through the medium of Adobe Pass Authentication [User Metadata Call](/help/authentication/user-metadata.md) and [Logout](/help/authentication/initiate-logout.md) services.


>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the tvOS implementation/s.
 

- The application would have to determine if the authentication has happened as a result of a sign-in through the platform SSO or not, using the "*tokenSource"* [user metadata](/help/authentication/user-metadata.md) from the Adobe Pass Authentication service.
- The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> Accounts -> TV Provider`* on tvOS **only** in case the *"tokenSource"* value is equal to "*Apple".*
- The application would have to [initiate the logout](/help/authentication/initiate-logout.md) from the Adobe Pass Authentication service using a direct HTTP call. This would not facilitate session clean-up on the MVPD side.

 

>[!TIP]
>
> **<u>Pro Tip:</u>** Follow the steps below for the iOS/iPadOS implementation/s.

- The application would have to determine if the authentication has happened as a result of a sign-in through the platform SSO or not,using the "*tokenSource"* [user metadata](/help/authentication/user-metadata.md) from the Adobe Pass Authentication service.
- The application would have to instruct/prompt the user to explicitly sign out from *`Settings -> TV Provider`* on iOS/iPadOS **only** in case the *"tokenSource"* value is equal to *"Apple"*.
- The application would have to [initiate the logout](/help/authentication/initiate-logout.md) from the Adobe Pass Authentication service using a [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) or a [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) component. This would facilitate session clean-up on the MVPD side.

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
