---
title: Android Application Registration
description: Android Application Registration
exl-id: 6238bd87-ac97-4a5c-9d92-3631f7b2d46a
---
# Android Application Registration {#android-application-registration}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

Starting with version 3.0 of the Android AccessEnabler SDK, we are changing the Authentication mechanism with Adobe's servers. Instead of using a public key and secret system to sign the requestorID, we are introducing the concept of a Software statement string that can be used to obtain an access token that is later used for all calls that the SDK makes to our servers. In adition to a software statement you will also need to create a deep link for your application.

For more information, see [Dynamic Client Registration](/help/authentication/dynamic-client-registration.md)

## What is a Software Statement? {#what}

A Software Statement is a JWT token that contains information about your application. Every application should have a unique software statement which is used by our servers to identify the application in Adobe's system. The Software Statement needs to be passed when you initialize the AccessEnabler SDK and it will be used to register the application with Adobe. Upon registration, the SDK will receive a client id and a client secret which will be used to obtain an access token. Any call that the SDK makes to our servers will require a valid access token. The SDK is responsible for registering the application, obtaining and refreshing the access token.

>[!NOTE]
>
>Software Statements are app-specific and an individual Software Statement cannot be used for more than one application. Please note that Programmer level software statements have the same constraint, they can only be used for single application, whether single channel or multi-channel.

## How to obtain a Software Statement? {#how-to-get-ss}

### If you have access to Adobe's TVE Dashboard:

* Open your browser and navigate to [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com).
* Navigate to `Channels` section and select your channel.
* Navigate to `Registered Applications` Tab.
* Click on `Add new application`.
* Provide a name and a version for your application and select the platforms on which it will be available. Android in our case.
* Provide a Domain Name by choosing from a list of domains already configured for your Programmer.
* Push your changes to the server and then navigate back to you Channel's Registered Applications tab.
* You should see a list with all registred applications. Select the **Download** button on the application that you've just created. You may need to wait a few minutes before your Software Statement it's ready for download.
* A text file will be downloaded. Use its contents as your Software Statement.

For more information, see [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

### If you don't have access to Adobe's TVE Dashboard:

Submit a ticket to `tve-support@adobe.com`. Please include all the necessary information like channel, application name, version and platforms and someone from our support team will create a software statement for you.

## How to use the Software Statement? {#how-to-use-ss}

After you obtain your Software Statement you need to pass it as a paramenter in the Access Enabler constructor. We recommend hosting the Software Statement on a remote location. This way, you can easily revoke and change the Software Statement whithout releasing a new version of your application.

## Create and use a deep link for your application {#create}

On Android, use as deep link value the reverse of the domain name selected when you created the Software Statement

Created deep link should have a unique value on the Android device. When multiple applications use the same deep link value, the authentication and logout flows will interfere.

## How to use the Software Statement and the deep link {#use-both}

In your application's resource file `strings.xml` add the following code:

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```
