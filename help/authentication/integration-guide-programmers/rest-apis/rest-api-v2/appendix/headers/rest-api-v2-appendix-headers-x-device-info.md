---
title: Header - X-Device-Info
description: REST API V2 - Header - X-Device-Info
exl-id: 0ef25e06-86de-427a-a938-7ba3817f0d5e
---
# Header - X-Device-Info {#header-x-device-info}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>X-Device-Info</b> request header contains the client information (device, connection and application) related to the actual streaming device and is used to determine platform-specific rules that MVPDs may enforce.

## Syntax {#syntax}

<table style="table-layout:auto">
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>X-Device-Info</b>: &lt;device_information&gt;</td>
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

<b>&lt;device_information&gt;</b>

The `Base64-encoded` value of the JSON element containing at least the attributes marked as required by the following table. 

<table style="table-layout:auto">
    <tr>
        <th style="background-color: #EFF2F7; width: 15%;">Presence</th>
        <th style="background-color: #EFF2F7; width: 15%;">Key</th>
        <th style="background-color: #EFF2F7;">Description</th>    
        <th style="background-color: #EFF2F7; width: 15%;">Restricted</th>
        <th style="background-color: #EFF2F7;">Possible Values</th>
    </tr>
    <tr>
        <td></td>
        <td>primaryHardwareType</td>
        <td>The device’s primary hardware type.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Camera</li>
                <li>DataCollectionTerminal</li>
                <li>Desktop</li>
                <li>EmbeddedNetworkModule</li>
                <li>eReader</li>
                <li>GamesConsole</li>
                <li>GeolocationTracker</li>
                <li>Glasses</li>
                <li>MediaPlayer</li>
                <li>MobilePhone</li>
                <li>PaymentTerminal</li>
                <li>PluginModem</li>
                <li>SetTopBox</li>
                <li>TV</li>
                <li>Tablet</li>
                <li>WirelessHotspot</li>
                <li>Wristwatch</li>
                <li>Unknown</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><i>required</i></td>
        <td>model</td>
        <td>The device’s model name.</td>
        <td></td>
        <td>e.g. iPhone, SM-G930V, AppleTV, etc.</td>
    </tr>
    <tr>
        <td><i>required</i></td>
        <td>version</td>
        <td>The device’s version.</td>
        <td></td>
        <td>e.g. 2.0.1, etc.</td>
    </tr>
    <tr>
        <td></td>
        <td>manufacturer</td>
        <td>The device’s manufacturing company/organization.</td>
        <td></td>
        <td>e.g. Samsung, LG, ZTE, Huawei, Motorola, Apple, etc.</td>
    </tr>
    <tr>
        <td></td>
        <td>vendor</td>
        <td>The device’s selling company/organisation.</td>
        <td></td>
        <td>e.g. Apple, Samsung, LG, Google, etc.</td>
    </tr>
    <tr>
        <td><i>required</i></td>
        <td>osName</td>
        <td>The device’s Operating System (OS) name.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Android</li>
                <li>Chrome OS</li>
                <li>Linux</li>
                <li>Mac OS</li>
                <li>OS X</li>
                <li>OpenBSD</li>
                <li>Roku OS</li>
                <li>Windows</li>
                <li>iOS</li>
                <li>tvOS</li>
                <li>webOS</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>osFamily</td>
        <td>The device’s Operating System (OS) group name.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Android</li>
                <li>BSD</li>
                <li>Linux</li>
                <li>PlayStation OS</li>
                <li>Roku OS</li>
                <li>Symbian</li>
                <li>Tizen</li>
                <li>Windows</li>
                <li>iOS</li>
                <li>tvOS</li>
                <li>macOS</li>
                <li>webOS</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>osVendor</td>
        <td>The device’s Operating System (OS) supplier.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Amazon</li>
                <li>Apple</li>
                <li>Google</li>
                <li>LG</li>
                <li>Microsoft</li>
                <li>Mozilla</li>
                <li>Nintendo</li>
                <li>Nokia</li>
                <li>Roku</li>
                <li>Samsung</li>
                <li>Sony</li>
                <li>Tizen Project</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><i>required</i></td>
        <td>osVersion</td>
        <td>The device’s Operating System (OS) version.</td>
        <td></td>
        <td>e.g. 10.2, 9.0.1, etc.</td>
    </tr>
    <tr>
        <td></td>
        <td>browserName</td>
        <td>The browser’s name.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Android Browser</li>
                <li>Chrome</li>
                <li>Edge</li>
                <li>Firefox</li>
                <li>Internet Explorer</li>
                <li>Opera</li>
                <li>Safari</li>
                <li>SeaMonkey</li>
                <li>Symbian Browser</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>browserVendor</td>
        <td>The browser’s building company/organisation.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>Amazon</li>
                <li>Apple</li>
                <li>Google</li>
                <li>Microsoft</li>
                <li>Motorola</li>
                <li>Mozilla</li>
                <li>Netscape</li>
                <li>Nintendo</li>
                <li>Nokia</li>
                <li>Samsung</li>
                <li>Sony Ericsson</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>browserVersion</td>
        <td>The device’s browser version.</td>
        <td></td>
        <td>e.g. 60.0.3112</td>
    </tr>
    <tr>
        <td></td>
        <td>userAgent</td>
        <td>The device’s user agent.</td>
        <td></td>
        <td>e.g. Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, like Gecko) Version/10.0.3 Safari/602.4.8</td>
    </tr>
    <tr>
        <td></td>
        <td>displayWidth</td>
        <td>The device’s physical screen width.</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td>displayHeight</td>
        <td>The device’s physical screen height.</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td>displayPpi</td>
        <td>The device’s physical screen pixel density.</td>
        <td></td>
        <td>e.g. 294</td>
    </tr>
    <tr>
        <td></td>
        <td>diagonalScreenSize</td>
        <td>The device’s physical screen diagonal dimension in inches.</td>
        <td></td>
        <td>e.g. 5.5, 10.1</td>
    </tr>
    <tr>
        <td></td>
        <td>connectionIp</td>
        <td>The device’s IP used for sending HTTP requests.</td>
        <td></td>
        <td>e.g. 8.8.4.4</td>
    </tr>
    <tr>
        <td></td>
        <td>connectionPort</td>
        <td>The device’s port used for sending HTTP requests.</td>
        <td></td>
        <td>e.g. 53124</td>
    </tr>
    <tr>
        <td><i>required</i></td>
        <td>connectionType</td>
        <td>The network connection type.</td>
        <td></td>
        <td>e.g. WiFi, LAN, 3G, 4G, 5G</td>
    </tr>
    <tr>
        <td></td>
        <td>connectionSecure</td>
        <td>The network connection security status.</td>
        <td>&check;</td>
        <td>
            The values are restricted:
            <ul>
                <li>true - in the case of a secure network</li>
                <li>false - in the case of a public hot spot</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>applicationId</td>
        <td>The application’s unique identifier.</td>
        <td></td>
        <td>e.g. REF30</td>
    </tr>
</table>


## Examples {#examples}

```JSON

// Device information
// {
//  "primaryHardwareType" : "MobilePhone",
//  "model":"SM-S901U",
//  "vendor":"samsung",
//  "version":"r0q",
//  "manufacturer":"samsung",
//  "osName":"Android",
//  "osVersion":"14"
// }
 
// BASE64-encoded
// ewogICJwcmltYXJ5SGFyZHdhcmVUeXBlIiA6ICJNb2JpbGVQaG9uZSIsCiAgIm1vZGVsIjoiU00tUzkwMVUiLAogICJ2ZW5kb3I
// iOiJzYW1zdW5nIiwKICAidmVyc2lvbiI6InIwcSIsCiAgIm1hbnVmYWN0dXJlciI6InNhbXN1bmciLAogICJvc05hbWUiOiJBbmRyb
// 2lkIiwKICAib3NWZXJzaW9uIjoiMTQiCn0=
 
X-Device-Info: ewogICJwcmltYXJ5SGFyZHdhcmVUeXBlIiA6ICJNb2JpbGVQaG9uZSIsCiAgIm1vZGVsIjoiU00tUzkwMVUiLAogICJ2ZW5kb3IiOiJzYW1zdW5nIiwKICAidmVyc2lvbiI6InIwcSIsCiAgIm1hbnVmYWN0dXJlciI6InNhbXN1bmciLAogICJvc05hbWUiOiJBbmRyb2lkIiwKICAib3NWZXJzaW9uIjoiMTQiCn0=
```

## Cookbooks {#cookbooks}

>[!IMPORTANT]
> 
> The code snippets and documentation resources are provided for referencing purposes. 
> 
> The code snippets are not exhaustive and may require additional modifications to work in your project.
>
> Regardless of your actual implementation, the `X-Device-Info` header must contain a value formatted as described in the [Directives](#directives) section.

### Browsers {#browsers}

For client applications running in a browser, the `X-Device-Info` header can be omitted as the browser will automatically send a minimal set of required information in the `User-Agent` header.

You can still use the `X-Device-Info` header to provide additional information about the device, connection, and application, in case your client application integrates a library or service that provides a device identification mechanism.   

### Mobile Devices {#mobile-devices}

#### iOS & iPadOS {#ios-ipados}

To build the `X-Device-Info` header for devices running [iOS or iPadOS](https://developer.apple.com/documentation/ios-ipados-release-notes), you may refer to the following documents and below code snippet:

* Apple developer documentation for [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice).
* Apple developer documentation for [Reachability](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html).
* Linux manual documentation for [uname](https://man7.org/linux/man-pages/man2/uname.2.html).

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"REF30" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

The device information can be constructed the following way:

| Key           | Source                 | Value (example) |
|---------------|------------------------|-----------------|
| model         | uname.machine          | iPhone          |
| vendor        | hardcoded              | Apple           |
| manufacturer  | hardcoded              | Apple           |
| version       | uname.machine          | 8,1             |
| displayWidth  | UIScreen.mainScreen    | 320             |
| displayHeight | UIScreen.mainScreen    | 568             |
| osName        | UIDevice.systemName    | iOS             |
| osVersion     | UIDevice.systemVersion | 10.2            |

The connection information can be constructed the following way:

| Key              | Source                                   | Value (example) |
|------------------|------------------------------------------|-----------------|
| connectionType   | [Reachability currentReachabilityStatus] |                 |
| connectionSecure |                                          |                 |


The application information can be constructed the following way:

| Key           | Source    | Value (example) |
|---------------|-----------|-----------------|
| applicationId | hardcoded | REF30           |

#### Android {#android}

To build the `X-Device-Info` header for devices running [Android](https://developer.android.com/about/versions), you may refer to the following documents and below code snippet:

* Android developer documentation for [Build](https://developer.android.com/reference/android/os/Build.html) class.

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model", Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer", Build.MANUFACTURER);
          clientInformation.put("version", Build.DEVICE);
          clientInformation.put("osName", "Android");
          clientInformation.put("osVersion", Build.VERSION.RELEASE);
          clientInformation.put("connectionType", connectionType);
          clientInformation.put("applicationId", "REF30");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

The device information can be constructed the following way:

| Key           | Source                      | Value (example) |
|---------------|-----------------------------|-----------------|
| model         | Build.MODEL                 | GT-I9505        |
| vendor        | Build.BRAND                 | samsung         |
| manufacturer  | Build.MANUFACTURER          | samsung         |
| version       | Build.DEVICE                | jflte           |
| displayWidth  | DisplayMetrics.widthPixels  | 600             |
| displayHeight | DisplayMetrics.heightPixels | 800             |
| osName        | hardcoded                   | Android         |
| osVersion     | Build.VERSION.RELEASE       | 5.0.1           |

The connection information can be constructed the following way:

| Key              | Source                                                                                                                                                        | Value (example)                                                                             |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| connectionType   | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
| connectionSecure |                                                                                                                                                               |                                                                                             |

The application information can be constructed the following way:

| Key           | Source    | Value (example) |
|---------------|-----------|-----------------|
| applicationId | hardcoded | REF30           |

### TV Connected Devices {#tv-connected-devices}

#### tvOS {#tvos}

To build the `X-Device-Info` header for devices running [tvOS](https://developer.apple.com/documentation/tvos-release-notes), you may refer to the following documents and below code snippet:

* Apple developer documentation for [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice).
* Apple developer documentation for [Reachability](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html).
* Linux manual documentation for [uname](https://man7.org/linux/man-pages/man2/uname.2.html).

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"REF30" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

The device information can be constructed the following way:

| Key           | Source                 | Value (example) |
|---------------|------------------------|-----------------|
| model         | uname.machine          | AppleTV         |
| vendor        | hardcoded              | Apple           |
| manufacturer  | hardcoded              | Apple           |
| version       | uname.machine          | 8,1             |
| displayWidth  | UIScreen.mainScreen    | 1920            |
| displayHeight | UIScreen.mainScreen    | 1080            |
| osName        | UIDevice.systemName    | tvOS            |
| osVersion     | UIDevice.systemVersion | 10.2            |

The connection information can be constructed the following way:

| Key              | Source                                   | Value (example) |
|------------------|------------------------------------------|-----------------|
| connectionType   | [Reachability currentReachabilityStatus] |                 |
| connectionSecure |                                          |                 |

The application information can be constructed the following way:

| Key           | Source    | Value (example) |
|---------------|-----------|-----------------|
| applicationId | hardcoded | REF30           |

#### Fire OS {#fireos}

To build the `X-Device-Info` header for devices running [Fire OS](https://developer.amazon.com/docs/fire-tv/fire-os-overview.html), you may refer to the following documents:

* Android developer documentation for [Build](https://developer.android.com/reference/android/os/Build.html) class.
* Amazon developer documentation for [Identifying Fire TV Devices](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html).

The device information can be constructed the following way:

| Key           | Source                      | Value (example) |
|---------------|-----------------------------|-----------------|
| model         | Build.MODEL                 | AFTM            |
| vendor        | Build.BRAND                 | Amazon          |
| manufacturer  | Build.MANUFACTURER          | Amazon          |
| version       | Build.DEVICE                | montoya         |
| displayWidth  | DisplayMetrics.widthPixels  |                 |
| displayHeight | DisplayMetrics.heightPixels |                 |
| osName        | hardcoded                   | Android         |
| osVersion     | Build.VERSION.RELEASE       | 5.1.1           |

The connection information can be constructed the following way:

| Key              | Source | Value (example) |
|------------------|--------|-----------------|
| connectionType   |        |                 |
| connectionSecure |        |                 |

The application information can be constructed the following way:

| Key           | Source    | Value (example) |
|---------------|-----------|-----------------|
| applicationId | hardcoded | REF30           |

#### Roku OS {#rokuos}

To build the `X-Device-Info` header for devices running [Roku OS](https://developer.roku.com/docs/developer-program/release-notes/roku-os-release-notes.md), you may refer to the following documents:

* Roku developer documentation for [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md).

The device information can be constructed the following way:

| Key           | Source                                     | Value (example) |
|---------------|--------------------------------------------|-----------------|
| model         | hardcoded                                  | "Roku"          |
| vendor        | ifDeviceInfo.GetModelDetails().VendorName  | "Sharp", "Roku" |
| manufacturer  | ifDeviceInfo.GetModelDetails().VendorName  | "Sharp", "Roku" |
| version       | ifDeviceInfo.GetModelDetails().ModelNumber | "5303X"         |
| displayWidth  | ifDeviceInfo.GetDisplaySize().w            | 1920            |
| displayHeight | ifDeviceInfo.GetDisplaySize().h            | 1080            |
| osName        | hardcoded                                  | "Roku"          |
| osVersion     | ifDeviceInfo.getVersion()                  |                 |

The connection information can be constructed the following way:

| Key               | Source                             | Value (example)                       |
|-------------------|------------------------------------|---------------------------------------|
| connectionType    | ifDeviceInfo.GetConnectionType()   | "WifiConnection", "WiredConnection"   |
| connectionSecure  | hardcoded                          | true if connection is wired           |

The application information can be constructed the following way:

| Key           | Source    | Value (example) |
|---------------|-----------|-----------------|
| applicationId | hardcoded | REF30           |

### Others {#others}

For device platforms not covered in the documentation, the client information (device, connection and application) should be linked to any available hardware and operating system (OS) attributes, typically specified in the device’s hardware and OS manuals.
