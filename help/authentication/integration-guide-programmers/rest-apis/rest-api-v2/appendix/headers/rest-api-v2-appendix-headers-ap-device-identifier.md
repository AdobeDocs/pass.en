---
title: Header - AP-Device-Identifier
description: REST API V2 - Header - AP-Device-Identifier
exl-id: 90a5882b-2e6d-4e67-994a-050465cac6c6
---
# Header - AP-Device-Identifier {#header-ap-device-identifier}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>AP-Device-Identifier</b> request header contains the streaming device identifier as it was created by the client application.

## Syntax {#syntax}

<table style="table-layout:auto">
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AP-Device-Identifier</b>: &lt;type&gt; &lt;identifier&gt;</td>
   </tr>
   <tr>
      <td>Header Type</td>
      <td>Request header</td>
   </tr>
   <tr>
      <td>Standard</td>
      <td>No</td>
   </tr>
</table>

## Directives {#directives}

<b>&lt;type&gt;</b>

The device identifier type.

There is only one supported types as presented below.

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7; width: 15%;">Type</th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td>fingerprint</td>
      <td>
            The device identifier consists of a stable and unique identifier created and managed by the client application for each device.
            <br/>
            The client application should cache the device identifier in persistent storage, as losing or altering it will invalidate authentication. The client application should prevent value changes caused by user actions such as application uninstallation, re-installation, or upgrades.
      </td>
   </tr>
</table>


<b>&lt;identifier&gt;</b>

The `Base64-encoded` value of the device identifier.

## Example {#example}

```JSON
// device identifier
// ba23d141-d715-561c-94f4-e9e4c966b1eb

// Base64-encoded
// YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi

AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
```

## Cookbooks {#cookbooks}

>[!IMPORTANT]
>
> The documentation resources are provided for referencing purposes.
>
> The documentation resources are not exhaustive and may require additional modifications to work in your project.
> 
> Regardless of your actual implementation, the `AP-Device-Identifier` header must contain a value formated as described in the [Directives](#directives) section.

### Browsers {#browsers}

To build the `AP-Device-Identifier` header for devices running in a browser, your client application requires to compute a stable and unique identifier based on available data such as browser, device, or user specific data.

_(*) We recommend to integrate a library or service that provides a browser or device fingerprinting mechanism._

### Mobile Devices {#mobile-devices}

#### iOS & iPadOS {#ios-ipados}

To build the `AP-Device-Identifier` header for devices running [iOS or iPadOS](https://developer.apple.com/documentation/ios-ipados-release-notes), you may refer to the following documents:

* Apple developer documentation for [identifierForVendor](https://developer.apple.com/documentation/uikit/uidevice/1620059-identifierforvendor).

_(*) We recommend to apply an SHA-256 hash function over the OS provided value._

#### Android {#android}

To build the `AP-Device-Identifier` header for devices running [Android](https://developer.android.com/about/versions), you may refer to the following documents:

* Android developer documentation for [ANDROID_ID](https://developer.android.com/reference/android/provider/Settings.Secure#ANDROID_ID).

_(*) We recommend to apply an SHA-256 hash function over the OS provided value._

### TV Connected Devices {#tv-connected-devices}

#### tvOS {#tvos}

To build the `AP-Device-Identifier` header for devices running [tvOS](https://developer.apple.com/documentation/tvos-release-notes), you may refer to the following documents:

* Apple developer documentation for [identifierForVendor](https://developer.apple.com/documentation/uikit/uidevice/1620059-identifierforvendor).

_(*) We recommend to apply an SHA-256 hash function over the OS provided value._

#### Fire OS {#fireos}

To build the `AP-Device-Identifier` header for devices running [Fire OS](https://developer.amazon.com/docs/fire-tv/fire-os-overview.html), you may refer to the following documents:

* Android developer documentation for [ANDROID_ID](https://developer.android.com/reference/android/provider/Settings.Secure#ANDROID_ID).

_(*) We recommend to apply an SHA-256 hash function over the OS provided value._

#### Roku OS {#rokuos}

To build the `AP-Device-Identifier` header for devices running [Roku OS](https://developer.roku.com/docs/developer-program/release-notes/roku-os-release-notes.md), you may refer to the following documents:

* Roku developer documentation for [GetChannelClientId](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getchannelclientid-as-string).

_(*) We recommend to apply an SHA-256 hash function over the OS provided value._

### Others {#others}

For device platforms not covered in the documentation, the device identifier should be linked to any available hardware identification, typically specified in the device’s hardware manual. 

If no hardware identifiers are available, a uniquely generated identifier based on client application attributes should be used and cached in persistent storage.
