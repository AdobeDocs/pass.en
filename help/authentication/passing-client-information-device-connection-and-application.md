---
title: Passing client information (device, connection, and application)
description: Passing client information (device, connection, and application)
exl-id: 0b21ef0e-c169-48ff-ac01-25411cfece1e
---
# Passing client information (device, connection, and application) {#pass-client-info}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Scope {#pass-client-info-scope}

This document aggregates details and cookbooks for passing client information (device, connection and application) from a Programmer application to Adobe Pass Authentication REST APIs or SDKs.

The benefits of providing client information are:

* The ability to properly enable Home Base Authentication (HBA) in the case of some device types and MVPDs that can support HBA.
* The ability to properly apply TTLs in the case of some device types (for example, configure longer TTLs for authentication sessions on TV connected devices).
* The ability to properly aggregate business metrics in broken down reports across device types using Entitlement Service Monitoring (ESM).
* Unblocks the ability to properly apply various business rules (ex. degradation) on specific device types.

## Overview {#pass-client-info-overview}

The client information consists of:

* **Device** information about the hardware and software attributes of the device from where the user is trying to consume the Programmer content.
* **Connection** information about the connection attributes of the device from where the user is connecting to Adobe Pass Authentication services and/or Programmer services (e.g. server-to-server implementations).
* **Application** information about the registered application from where the user is trying to consume the Programmer content.

The client information is a JSON object built with keys presented in the following table.

>[!NOTE]
>
>The following **keys** are **mandatory** to be sent in the client information JSON object: **model**, **osName**.
>
>The following keys have **restricted** values: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|   |Key                                | Restricted |                                                  Description                                               |                                                                                                                                                                                   Possible Values                                                                                                                                                                                 |
|---|---|---|---|---|
|            | primaryHardwareType | # Yes      |               The device's primary hardware type.                                  |               # The values are restricted:                                                                     Camera                                                      DataCollectionTerminal                                                      Desktop                                                      EmbeddedNetworkModule                                                      eReader                                                      GamesConsole                                                      GeolocationTracker                                                      Glasses                                                      MediaPlayer                                                      MobilePhone                                                      PaymentTerminal                                                      PluginModem                                                      SetTopBox                                                      TV                                                      Tablet                                                      WirelessHotspot                                                      Wristwatch                                                      Unknown                                            |
| #mandatory |               model                         | No         |               The device's model name.                                             | e.g. iPhone, SM-G930V, AppleTV, etc.                                                                                                                                                                                                                                                                                                                      |
|            | version             | No         | The device's version.                                      | e.g. 2.0.1, etc.                                                                                                                                                                                                                                                                                                                                          |
|            | manufacturer        | No         | The device's manufacturing company/organization.           | e.g. Samsung, LG, ZTE, Huawei, Motorola, Apple, etc.                                                                                                                                                                                                                                                                                                      |
|            |               vendor                        | No         |               The device's selling company/organisation.                           | e.g. Apple, Samsung, LG, Google, etc.                                                                                                                                                                                                                                                                                                                     |
| #mandatory | osName              | # Yes      |               The device's Operating System (OS) name.                             |               # The values are restricted:                                                   Android                   Chrome OS                   Linux                   Mac OS                   OS X                   OpenBSD                   Roku OS                   Windows                   iOS                   tvOS                   webOS                                                                                                                                                                                                                                           |
|            | osFamily            | Yes        |               The device's Operating System (OS) group name.                       |               # The values are restricted:                                                   Android                   BSD                   Linux                   PlayStation OS                   Roku OS                   Symbian                   Tizen                   Windows                   iOS                   macOS                   tvOS                   webOS                                                                                                                                                                                                                                |
|            | osVendor            | No         | The device's Operating System (OS) supplier.               |                                 Amazon                   Apple                   Google                   LG                   Microsoft                   Mozilla                   Nintendo                   Nokia                   Roku                   Samsung                   Sony                   Tizen Project                                                                                                                                                                                                                                                                 |
|            | osVersion           | No         | The device's Operating System (OS) version.                | e.g. 10.2, 9.0.1, etc.                                                                                                                                                                                                                                                                                                                                    |
|            | browserName         | # Yes      |               The browser's name.                                                  |               # The values are restricted:                                                   Android Browser                   Chrome                   Edge                   Firefox                   Internet Explorer                   Opera                   Safari                   SeaMonkey                   Symbian Browser                                                                                                                                                                                                                                         |
|            | browserVendor       | # Yes      |               The browser's building company/organisation.                         |               # The values are restricted:                                                   Amazon                   Apple                   Google                   Microsoft                   Motorola                   Mozilla                   Netscape                   Nintendo                   Nokia                   Samsung                   Sony Ericsson                                                                                                                                                                                                                                     |
|            | browserVersion      | No         | The device's browser version.                              |               e.g. 60.0.3112                                                                                                                                                                                                                                                                                                                                                                  |
|            | userAgent           | No         | The device's user agent.                                   | e.g. Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, like Gecko) Version/10.0.3 Safari/602.4.8                                                                                                                                                                                                                                |
|            | displayWidth        | No         | The device's physical screen width.                        |                                                                                                                                                                                                                                                                                                                                                           |
|            | displayHeight       | No         |               The device's physical screen height.                                 |                                                                                                                                                                                                                                                                                                                                                           |
|            | displayPpi          | No         | The device's physical screen pixel density.                | e.g. 294                                                                                                                                                                                                                                                                                                                                                  |
|            | diagonalScreenSize  | No         | The device's physical screen diagonal dimension in inches. | e.g. 5.5, 10.1                                                                                                                                                                                                                                                                                                                                            |
|            | connectionIp        | No         | The device's IP used for sending HTTP requests.            | e.g. 8.8.4.4                                                                                                                                                                                                                                                                                                                                              |
|            | connectionPort      | No         | The device's port used for sending HTTP requests.          | e.g. 53124                                                                                                                                                                                                                                                                                                                                                |
|            | connectionType      | No         |               The network connection type.                                         |               e.g. WiFi, LAN, 3G, 4G, 5G                                                                                                                                                                                                                                                                                                                                          |
|            | connectionSecure    | # Yes      |               The network connection security status.                              |               # The values are restricted:                                                   true - in the case of a secure network                   false - in the case of a public hot spot                                                                                                                                                                                                                                                        |
|            | applicationId       | No         | The application's unique identifier.                       | e.g. CNN                                                                                                                                                                                                                                                                                                                                                  |

## API references {#api-ref}

This section presents the API responsible for handling client information when using Adobe Pass Authentication REST APIs or SDKs.

### REST API {#rest-api}

Adobe Pass Authentication services support receiving the client information in the following ways:

* As a **header: "X-Device-Info"**
* As a **query parameter: "device_info"**
* As a **post parameter: "device_info"**

>[!IMPORTANT]
>
>In all three scenarios, the payload of the header or parameter must be **Base64 encoded and URL encoded**.

**SDK**

#### JavaScript SDK {#js-sdk}

The AccessEnabler JavaScript SDK builds by default a client information JSON object, which will be passed to Adobe Pass Authentication services, unless overridden.

The AccessEnabler JavaScript SDK supports **overriding only** the "applicationId" key from the client information JSON object through the [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))'s *applicationId* options parameter.

>[!CAUTION]
>
>The `applicationId` parameter value must be a plain text String value.
>In case the Programmer application decides to pass the applicationId, then the rest of client information keys will still be computed by the AccessEnabler JavaScript SDK.

#### iOS/tvOS SDK {#ios-tvos-sdk}

The AccessEnabler iOS/tvOS SDK builds by default a client information JSON object, which will be passed to Adobe Pass Authentication services, unless overridden.

The AccessEnabler iOS/tvOS SDK supports **overriding the whole** client information JSON object through the [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)'s device_info parameter.

>[!CAUTION]
>
>The *device_info* parameter value must be a **Base64 encoded** *NSString* value.
>
>In case the Programmer application decides to pass the *device_info*, then all client information keys computed by the AccessEnabler iOS/tvOS SDK will be overridden. Therefore, it is very important to compute and pass the values for as many keys as possible. For more details regarding the implementation, see the [Overview](#pass-client-info-overview) table and the [iOS/tvOS cookbook](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

The `AccessEnabler` Android/FireOS SDK builds by default a client information JSON object, which will be passed to Adobe Pass Authentication services, unless overridden.

The `AccessEnabler` Android/FireOS SDK supports **overriding the whole** client information JSON object through the [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)'s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)'s `device_info` parameter.

>[!NOTE]
>
>The `device_info` parameter value must be a **Base64 encoded** String value.

>[!IMPORTANT]
>
>In case the Programmer application decides to pass the `device_info`, then all client information keys computed by the `AccessEnabler` Android/FireOS SDK will be overridden. Therefore, it is very important to compute and pass the values for as many keys as possible. For more details regarding the implementation, see the [Overview](#pass-client-info-overview) table and the [Android](#android) and [FireOS](#fire-tv) cookbook.

## Cookbooks {#cookbooks}

This section presents a cookbook for building the client information JSON Object in the case of different device types.

>[!IMPORTANT]
>
>The keys which are marked with  **&#33;** are mandatory to be sent.

### Android {#android}

The device information can be constructed the following way:

|   | Key           | Source                      | Value (example)  |
|---|---------------|-----------------------------|---------------|
| &#33; | model         | Build.MODEL                 | GT-I9505      |
|   | vendor        | Build.BRAND                 | samsung       |
|   | manufacturer  | Build.MANUFACTURER          | samsung       |
| &#33; | version       | Build.DEVICE                | jflte         |
|   | displayWidth  | DisplayMetrics.widthPixels  | 600           |
|   | displayHeight | DisplayMetrics.heightPixels | 800           |
| &#33; | osName        | hardcoded                   | Android       |
| &#33; | osVersion     | Build.VERSION.RELEASE       | 5.0.1         |

The connection information can be constructed the following way:

|   | Key              | Source                                                                                                                                                    | Value (example)                                                                              |
|---|---|---|---|
| &#33;  | connectionType   | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|   | connectionSecure |                                                                                                                                                           |                                                                                           |

The application information can be constructed the following way:

|   | Key           | Source    | Value (example) |
|---|---------------|-----------|--------------|
|   | applicationId | hardcoded | CNN          |

>[!IMPORTANT]
>
>The device, connection and application information must be added to the same JSON object. Afterwards, the resulting object must be **Base64 encoded**. Also, in the case of Adobe Pass Authentication REST APIs, the value must be **URL encoded**.

**Sample code**

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
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
>
>**Resources:**
>* public class [build](https://developer.android.com/reference/android/os/Build.html){target=_blank} in Java developers' documentation.

### FireTV {#fire-tv}

The device information can be constructed the following way:

|   | Key           | Source                      | Value (e.g.) |
|---|---------------|-----------------------------|--------------|
| &#33; | model         | Build.MODEL                 | AFTM         |
|   | vendor        | Build.BRAND                 | Amazon       |
|   | manufacturer  | Build.MANUFACTURER          | Amazon       |
| &#33; | version       | Build.DEVICE                | montoya      |
|   | displayWidth  | DisplayMetrics.widthPixels  |              |
|   | displayHeight | DisplayMetrics.heightPixels |              |
| &#33; | osName        | hardcoded                   | Android      |
| &#33; | osVersion     | Build.VERSION.RELEASE       | 5.1.1        |

The connection information can be constructed the following way:

|   | Key              | Source | Value (example)  |
|---|------------------|--------|---------------|
| &#33; | connectionType   |        |               |
|   | connectionSecure |        |               |

The application information can be constructed the following way:

|   | Key           | Source    | Value (example) |
|---|---------------|-----------|--------------|
|   | applicationId | hardcoded | CNN          |

>[!IMPORTANT]
>
>The device, connection and application information must be added to the same JSON object. Afterwards, the resulting object must be **Base64 encoded**. Also, in the case of Adobe Pass Authentication REST APIs,  the value must be **URL encoded**.

>[!NOTE]
>
>**Resources:**
>* public class [Build](https://developer.android.com/reference/android/os/Build.html){target=_blank} in Android developers' documentation.
>* [Identifying FireTV devices](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}

### iOS/tvOS {#ios-tvos}

The device information can be constructed the following way:

|   | Key           | Source                 | Value (example) |
|---|---------------|------------------------|--------------|
| &#33; | model         | uname.machine          | iPhone       |
|   | vendor        | hardcoded              | Apple        |
|   | manufacturer  | hardcoded              | Apple        |
| &#33; | version       | uname.machine          | 8,1          |
|   | displayWidth  | UIScreen.mainScreen    | 320          |
|   | displayHeight | UIScreen.mainScreen    | 568          |
| &#33; | osName        | UIDevice.systemName    | iOS          |
| &#33; | osVersion     | UIDevice.systemVersion | 10.2         |

The connection information can be constructed the following way:

|   | Key              | Source                                    | Value (example) |
|---|------------------|-------------------------------------------|--------------|
| &#33; | connectionType   | [Reachability  currentReachabilityStatus] |              |
|   | connectionSecure |                                           |              |


The application information can be constructed the following way:

|   | Key           | Source    | Value (example) |
|---|---------------|-----------|--------------|
|   | applicationId | hardcoded | CNN          |

>[!IMPORTANT]
>
>The device, connection and application information must be added to the same JSON object. Afterwards, the resulting object must be Base64 encoded. Also, in the case of Adobe Pass Authentication REST APIs, the value must be URL encoded.

**Sample code**

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
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
>
>**Resources:**
>* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
>* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
>* [About Reachability](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}

### Roku {#roku}

The device information can be constructed the following way:

| Key | Source        | Value (example)                               |                 |
|-----|---------------|--------------------------------------------|-----------------|
| &#33;   | model         | hardcoded                                  | "Roku"          |
|     | vendor        | ifDeviceInfo.GetModelDetails().VendorName  | "Sharp", "Roku" |
|     | manufacturer  | ifDeviceInfo.GetModelDetails().VendorName  | "Sharp", "Roku" |
| &#33;   | version       | ifDeviceInfo.GetModelDetails().ModelNumber | "5303X"         |
|     | displayWidth  | ifDeviceInfo.GetDisplaySize().w            | 1920            |
|     | displayHeight | ifDeviceInfo.GetDisplaySize().h            | 1080            |
| &#33;   | osName        | hardcoded                                  | "Roku"          |
| &#33;   | osVersion     | ifDeviceInfo.getVersion()                  |                 |

The connection information can be constructed the following way:

|   |        Key       |              Source              |             Value (example)            |
|---|---|---|---|
| &#33; | connectionType   | ifDeviceInfo.GetConnectionType() | "WifiConnection", "WiredConnection" |
|   | connectionSecure | hardcoded                        | true if connection is wired         |

The application information can be constructed the following way:

|   | Key           | Source    | Value (example) |
|---|---------------|-----------|--------------|
|   | applicationId | hardcoded | CNN          |

>[!IMPORTANT]
>
>The device, connection and application information must be added to the same JSON object. Afterwards, the resulting object must be **Base64 encoded**. Also, in the case of Adobe Pass Authentication REST APIs, the value must be URL encoded.

>[!NOTE]
>
>For more information, see [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

The device information can be constructed the following way:

|   |                    Key                  |                                   Source                                 |               Value (example)              |
|---|---|---|---|
| &#33; |               model                     |               EasClientDeviceInformation.SystemProductName               |                 |
|   |               vendor                    | hardcoded                                        | Microsoft       |
|   |               manufacturer              | hardcoded                                        | Microsoft       |
| &#33; |               version                   | EasClientDeviceInformation.SystemHardwareVersion |                 |
|   | displayWidth    | DisplayInformation.ScreenWidthInRawPixels        | 1920            |
|   | displayHeight   | DisplayInformation.ScreenHeightInRawPixels       | 1080            |
| &#33; |               osName                    | EasClientDeviceInformation.OperatingSystem       |                 |
| &#33; | osVersion       | EasClientDeviceInformation.SystemFirmwareVersion |                 |

The connection information can be constructed the following way:

|   |        Key                    |                       Source                      |                   Example                   |
|---|---|---|---|
| &#33; |               connectionType              |                                                   |                   |
|   | connectionSecure  | NetworkAuthenticationType | "None", "Wpa" etc |

The application information can be constructed the following way:

|                   Key                 |               Source              |               Value (example)              |
|---|---|---|
| applicationId | hardcoded | CNN             |

>[!IMPORTANT]
>
>The device, connection and application information must be added to the same JSON object. Afterwards, the resulting object must be **Base64 encoded**. Also, in the case of Adobe Pass Authentication REST APIs, the value must be **URL encoded**.

**Resources**

* [EasClientDeviceInformation Class](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [DisplayInformation Class](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)
