---
title: Debugging the AccessEnabler iOS/tvOS SDK using Console app logs
description: Debugging the AccessEnabler iOS/tvOS SDK using Console app logs
exl-id: 0dad325e-db15-4ea0-a87a-75409eaf8d46
---
# (Legacy) Debugging the AccessEnabler iOS/tvOS SDK using Console app logs {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Overview

The scope of this document is to capture and present the evolution of AccessEnabler's iOS/tvOS SDK logging mechanism alongside some useful details for debugging the AccessEnabler framework using the Console app logs.

## Logging Mechanism State

The AccessEnabler iOS/tvOS logging mechanism purpose is to emit useful messages for troubleshooting possible issues which an application using the AccessEnabler framework could encounter due to it.

### AccessEnabler iOS/tvOS 3.5.0 and above

Starting with AccessEnabler iOS/tvOS 3.5.0 version the logging mechanism introduces the following improvements as changes:

*   AccessEnabler framework uses Apple's recommended [OSLog](https://developer.apple.com/documentation/os/oslog) implementation.

*   AccessEnabler framework introduces the ability to filter Console app logs based on Subsystem: **com.adobe.pass.AccessEnabler**. All messages emitted by the SDK are part of com.adobe.pass.AccessEnabler.

*   AccessEnabler framework introduces the ability to filter Console app logs based on Any (prefix): **[AccessEnabler]**. All messages emitted by the SDK are prefixed with [AccessEnabler].

*   AccessEnabler framework introduces the ability to filter Console app logs based on Category: **debug**, **error** in conjunction with any of the above two criterias: Subsystem or Any (prefix).

## Debugging using Console app logs

Depending on the issues which are investigated you may wish to include or exclude the logging messages emitted by the AccessEnabler framework, therefore you can find below some useful details which may help you during investigations and when using Console app logs.


### AccessEnabler iOS/tvOS 3.5.0 and above

#### Including {#including}

First of all in order to be able to see any of the logging messages emitted by the AccessEnabler framework you **must** select the "Include Info Messages" and "Include Debug Messages" in the Action section of the Console app, as presented in the image below.

![](../../../assets/include-info-debug-msg.png)


In order to be able to debug the functionality of the AccessEnabler iOS/tvOS SDK and **see** the AccessEnabler framework logs you can:

* Search in Console app using **Subsystem** option which Equals the com.adobe.pass.AccessEnabler value as in the image below.

![](../../../assets/subsys-console-app.png)

* Search in Console app using **Any** option which Contains the
  [AccessEnabler] value as in the image below.

![](../../../assets/any-optn-console-app.png)

Alongside the above two criterias you can also use the **Category** option in conjuction with **Subsystem** or **Any (prefix)** to explicitly search for **debug** or **error** level messages emitted by the AccessEnabler iOS/tvOS SDK.

#### Excluding

In order to be able to better debug the functionality of other components and **exclude** the AccessEnabler framework logs you can:

* Search in Console app using **Subsystem** option which Does not equal the com.adobe.pass.AccessEnabler value.
* Search in Console app using **Any** option which Does not contain the [AccessEnabler] value.

## Reporting an issue

When you are reporting an issue to Adobe Pass Authentication please consider the following suggestions:

* please try to provide the reproduction steps.
* please try to provide the OS version/s and device model/s on which the issue occurs.
* please try to provide the version of the AccessEnabler iOS/tvOS SDK experiencing the issue.
* please try to capture and attach all AccessEnabler iOS/tvOS SDK logging messages using either of the two options presented in the [Including](#including) section.
