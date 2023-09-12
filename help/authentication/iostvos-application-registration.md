---
title: iOS/tvOS Application Registration
description: iOS/tvOS Application Registration
exl-id: 89ee6b5a-29fa-4396-bfc8-7651aa3d6826
---
# iOS/tvOS Application Registration {#iostvos-application-registration}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Intro}

Starting with version 3.0 of the iOS/tvOS AccessEnabler SDK, we are changing the Authentication mechanism with Adobe's servers. Instead of using a public key and secret system to sign the requestorID, we are introducing the concept of a Software statement string that can be used to obtain an access token that is later used for all calls that the SDK makes to our servers. In addition to a software statement you will also need a custom URL scheme for your application.

For more information, see [Dynamic Client Registration](/help/authentication/dynamic-client-registration.md)

## What is a Software Statement? {#Soft_state}

A Software Statement is a JWT token that contains information about your application. Every application should have a unique software statement which is used by our servers to identify the application in Adobe's system. The Software Statement needs to be passed when you initialize the AccessEnabler SDK and it will be used to register the application with Adobe. Upon registration, the SDK will receive a client id and a client secret which will be used to obtain an access token. Any call that the SDK makes to our servers will require a valid access token. The SDK is responsible for registering the application, obtaining and refreshing the access token.

**Note:** A Software Statement is app-specific and same software statement cannot be used on more than one application. Please note that, Programmer level software statements also follows the same i.e. they can only be used for single application - whether single channel or multi-channel. This limitation also applies to custom scheme.

## How to obtain a Software Statement? {#obtain}

### If you have access to Adobe's TVE Dashboard:

- Open your browser and navigate to <https://console.auth.adobe.com>
- Navigate to `Channels` section and select your channel.
- Navigate to `Registered Applications` Tab.
- Click on `Add new application`.
- Provide a name and a version for your application and select the   platforms on which it will be available. iOS/tvOS in our case.
- Push your changes to the server and then navigate back to your Channel's Registered Applications tab.
- You should see a list with all registered applications. Click the   `Download` button on the application that you've just created. You may need to wait a few minutes before your Software Statement it's ready for download.
- A text file will be downloaded. Use it's contents as your Software Statement.

For more information see, [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### If you don't have access to Adobe's TVE Dashboard:

Submit a ticket to <tve-support@adobe.com>. Please include all the necesary information like channel, application name, version and platforms and someone from our support team will create a software statement for you.

## How to use the Software Statement? {#use}

After you obtain your Software Statement you need to pass it as a paramenter in the Access Enabler constructor. We recommend hosting the Software Statement on a remote location. This way, you can easily revoke and change the Software Statement whithout releasing a new version of your application.

## Generating a custom URL scheme for your application {#generating}

### If you have access to Adobe's TVE Dashboard:

- Open your browser and navigate to <https://console.auth.adobe.com>
- Navigate to `Channels` section and select your channel.
- Navigate to `Custom Schemes` Tab.
- Click on `Generate a new custom scheme`.
- A new custom scheme will be generated for your application. Ex: `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- Push your changes to the server.

### If you don't have access to Adobe's TVE Dashboard:

Submit a ticket to <tve-support@adobe.com>. Please include channel id and someone from our support team will create a custom scheme for you.

## How to use the custom Scheme {#use_custom}

In your application's `info.plist` file add the following code:

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
