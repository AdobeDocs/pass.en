---
title: Minimum System Requirements
description: Minimum System Requirements
exl-id: 57b21e2a-abd7-4b4b-85f1-25584a850e40
---
# Minimum System Requirements {#minimum-system-requirements}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Overview {#overview}

This document presents the current software and hardware requirements for implementing Adobe Pass Authentication integrations on supported platforms. All supported web/mobile browsers and operating systems listed below will benefit from the full support of Adobe Pass Authentication team, bound to the agreed SLAs.

While as Adobe Pass Authentication team we encourage the usage of the latest stable versions of the browsers and operating systems; we also acknowledge the existance of incompliant/older platforms and browsers that are currently in use. These outdated devices still may function without problems, however they will be more error-prone.

Initial approach to mitigate any issues appearing on these outdated platforms should be upgrading to the latest versions; this can be the OS version, browser version, or the version of the installed application.

Any issues appearing on these platforms will be addressed as a best-effort basis by the Adobe Pass Authentication team. 

Adobe Pass encourages our customers and partners to consider upgrading to the latest versions to benefit from Adobe's full support in any potential issues, in addition to performance, efficiency and security improvements. 


## Browser & Operating System Requirements {#browser-OS-system-requirements}


| Web/Mobile Browser (&#8224;)  | Supported Versions  |
|---|---|
|  Google Chrome | **70** or later  |
|  Mozilla Firefox| **57** or later  |
|  Apple Safari | **14** or later    |
|  Microsoft Edge |  **100** or later   |

(&#8224;) Adobe advises against using private or incognito mode.

| Operating system  | Supported Versions |
|---|---|
| *Android*  | **7.0** (Nougat) or later |
| *iOS*  | **14** or later  |
|  *iPadOS* | **14** or later   |
| *tvOS*  | **14** or later  |
|  *Fire OS* | **5 (Android 5.1)** or later   |
|  *Mac OS* | **10.13** or later  |
| *Microsoft Windows*   | **10** or later  |




>[!NOTE] 
>
>3rd-party Cookies - Adobe Pass Authentication entitlement flows might fail when 3rd-party cookies are disabled.  This issue only comes in to play when browser settings are modified. For all supported browsers, Adobe Pass Auuthentication should be functional with the default settings.  
 

## Device Requirements for Clientless (REST) Implementations {#general_clientless_reqs}

 
Any device that will consume Adobe Pass Authentication services through clientless implementations **must be able to**:

* Provide a unique, hashed device ID. If the device does not provide a unique hashed device ID, then it must be able to persist a unique ID provided by Adobe Pass Authentication. The device should be able to persist the unique ID permanently in its local storage and provide the unique ID as the Device ID when making calls to the Adobe Pass Authentication APIs.
* Generate digital signatures using the HMAC-SHA1 algorithm
* Set arbitrary HTTP headers
* Consume RESTful web services
* Parse XML and JSON data formats
* Send traffic using HTTPS
* Handle HTTP error codes
