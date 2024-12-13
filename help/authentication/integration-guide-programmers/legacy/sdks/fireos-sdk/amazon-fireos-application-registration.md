---
title: Amazon FireOS Application Registration
description: Amazon FireOS Application Registration
exl-id: 650fd4a2-dfc3-4c74-9b5b-6bea832a28ca
---
# (Legacy) Amazon FireOS Application Registration {#amazon-fireos-application-registration}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#intro}

Starting with version 3.0 of the FireOS AccessEnabler SDK, we are changing the Authentication mechanism with Adobe's servers. Instead of using a public key and secret system to sign the requestorID, we are introducing the concept of a Software Statement string that can be used to obtain an access token that is later used for all calls that the SDK makes to our servers. In adition to a Software Statement you will also need to create a deep link for your application.

More information, see [Dynamic Client Registration Overview](../../../rest-apis/rest-api-dcr/dynamic-client-registration-overview.md).

## What is a Software Statement? {#what}

A Software Statement is a JWT token that contains information about your application. Every application should have a unique Software Statement which is used by our servers to identify the application in Adobe's system. The Software Statement needs to be passed when you initialize the AccessEnabler SDK and it will be used to register the application with Adobe. Upon registration, the SDK will receive a client id and a client secret which will be used to obtain an access token. Any call that the SDK makes to our servers will require a valid access token. The SDK is responsible for registering the application, obtaining and refreshing the access token.

**Note:** Software Statements are app-specific and an individual Software Statement cannot be used for more than one application. Please note that this also applies to applications that offer access to multiple channels.

## How to obtain a Software Statement? {#how-to}

### If you have access to Adobe's TVE Dashboard:

1. Open your browser and navigate to `https://experience.adobe.com/#/pass/authentication`.

1. Navigate to the **[!UICONTROL Channels]** section, then select your channel.

1. Navigate to the **[!UICONTROL Registered Applications]** tab.

1. Click **[!UICONTROL Add new application]**.

1. Provide a name and a version for your application and select the platforms on which it will be available (such as Android).

1. Provide a **[!UICONTROL Domain Name]** by choosing from a list of domains already configured for your Programmer.

1. Push your changes to the server, then navigate back to you channel's **[!UICONTROL Registered Applications]** tab.

    You should see a list with all registered applications. 

1. Click **[!UICONTROL Download]** on the application that you've just created. 

    You may need to wait a few minutes before your Software Statement is ready for download.

    A text file downloads. Use its contents as your Software Statement.

More information, see [Dynamic Client Registration Management](../../../rest-apis/rest-api-dcr/dynamic-client-registration-overview.md#dynamic-client-registration-management).

### If you don't have access to Adobe's TVE Dashboard:

Submit a ticket to [tve-support@adobe.com](mailto:tve-support@adobe.com). Include all the necessary information, including channel, application name, version and platforms and someone from our support team will create a software statement for you.

## How to use the Software Statement {#use}

After you obtain your Software Statement, you need to pass it as a parameter in the Access Enabler constructor. Adobe recommends hosting the Software Statement on a remote location. This way, you can easily revoke and change the Software Statement without releasing a new version of your application.

## How to use the Software Statement {#use-both}

In your application's resource file `strings.xml` add the following code:

```XML
<string name="software_statement">softwarestatement value</string>
```
