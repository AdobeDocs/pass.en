---
title: iOS/tvOS v3.x Migration Guide
description: iOS/tvOS v3.x Migration Guide
exl-id: 4c43013c-40af-48b7-af26-0bd7f8df2bdb
---
# (Legacy) iOS/tvOS v3.x Migration Guide {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!TIP] 
> 
> **Notes:** 
>
> - Starting with iOS sdk version 3.1, implementors can now use WKWebView or UIWebView interchangeably. Since UIWebView is deprecated, apps should migrate to  to WKWebView, to avoid issues with future iOS versions. 
> - Note that migration would imply simply switching the UIWebView class with WKWebView, there is no specific work to be done in regards to Adobe's AccessEnabler.

</br>

## Update build settings {#update}

This release contains functionality written in SWIFT language. If your app is entirely Objective-C, you need to set the "Always Embed Swift Standard Libraries" checkbox in your target's build settings to "Yes". When this option is set, Xcode scans the bundled frameworks in your app and, if any of them contains Swift code, it copies the pertinent libraries into your app's bundle. If you do not update the build settings, your app might crash with errors stating that it cannot load AccessEnabler.framework or various `ibswift*` libraries.

</br>

## Adding your software statement {#add}

> For information on how to obtain your software statement go to this
> page:
> [Application Registration](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-application-registration.md)

Once you have your software statement we recommend hosting it on a remote server so you can easily revoke it or change it whithout deploying a new version of the application in the App Store. When the application starts, obtain your software statement from the remote location and pass it in the AccessEnabler constructor:

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> API info here: [iOS / tvOS API Reference](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)

</br>

## Add the custom URL scheme {#add-custom}

> For information on how to obtain a custom URL scheme go to this page: [Obtain a customer URL scheme](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-application-registration.md)

After you obtain the custom URL scheme you need to add it to the application's info.plist file. The custom scheme has this format: `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. You need to omit the colon and the forward slashes when adding it to the file. The above example will become `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist

    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>

```

</br>

## Intercepting calls on the custom URL scheme {#intercept}

This applies only in case your application previously enabled manual Safari View Controller (SVC) handling via the [setOptions(\["handleSVC":true"\])](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md) call and for specific MVPDs requiring Safari View Controller (SVC), therefore requiring loading the URLs of the authentication and logout endpoints by a SFSafariViewController controller instead of a UIWebView/WKWebView controller.

During authentication and logout flows your application must monitor the activity of the `SFSafariViewController `controller as it goes through several redirects. Your application must detect the moment when it loads a specific custom URL defined by your `application's custom URL scheme` (e.g.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. When the controller loads this specific custom URL your application must close the `SFSafariViewController` and call AccessEnabler's `handleExternalURL:url `API method.

In your `AppDelegate` add the following method:

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> API info here: [Handle External URL](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)

</br>

## Update the setRequestor method signature {#update-setreq}

Because the new SDK is using a new authentication mechanism, there is no need for the signedRequestId parameter or the public key and secret (for tvOS). The `setRequestor` method is simplified and it only needs the requestorID.

### iOS

This code:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

becomes:

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

This code:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

becomes:

```swift
    accessEnabler.setRequestor(requestorId)
```

> API info here: [Set Requestor](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)

</br>

## Replace getAuthenticationToken method with handleExternalURL method {#replace}

`getAuthentication` method was used in the past for completing the authentication flow. Since it's name was misleading, it was renamed to `handleExternalURL` and takes the url as a parameter.

Change all occurences of this:

```swift
    accessEnabler.getAuthenticationToken()
```

into this:

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> API info here: [Handle External URL](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)
