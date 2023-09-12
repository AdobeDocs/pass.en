---
title: REST API Overview
description: Overview for Rest APIs
exl-id: 5533d852-f644-417e-bf80-6f7aa1edd6b2
---
# REST API Overview {#rest-api-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Overview {#over}

The Adobe Primetime authentication REST API provides direct access to the TV Everywhere (TVE) authentication and authorization services. This API supports two primary architectures: Server-to-Server or Connected Devices (e.g. game consoles, Smart TVs, set-top boxes, etc.) applications that do not have web browsing capabilities. 

 

### Server-to-Server

Server-to-Server solutions involve Programmer client applications that integrate with Programmer services that connect with Adobe Primetime authentication services for TVE flows. This approach shifts most of TVE implementation from the client to the server where a single, unified authorization module can be built and maintained. The primary remaining responsibility of the client applications is the management of a web view for user authentication.

 

### Connected Devices

Connected Devices apps communicate directly with Primetime Authentication through the REST APIs to perform configuration, registration, authentication status checks and authorization flows, while a second screen (browser) app is required for the authentication flow. As such, native SDKs are not used.

 

### Other Architectures

In addition to the two primary REST API based architectures, Server-to-server and Direct client solutions for smart devices, there are other architectures.  Primary among them is the SDK architecture, which uses a client component called the Access Enabler that Primetime authentication provides to Programmers.  The app uses Access Enabler APIs to handle startup, authentication, authorization, and logout.  All communication between the Programmer's app and the Primetime authentication servers occurs through the Access Enabler.  A different flavor of Access Enabler is available for the following platforms: JavaScript, iOS, tvOS, Android and FireTV.

Although it is possible to use the REST API directly on client platforms that support native SDKs outside of a Server-to-Server solution, this approach is not recommended.

 

## REST API Pros and Cons {#ProsAndCons}

The Adobe Primetime Authentication REST API was created to provide a TV Everywhere (TVE) solution for devices that do not have web browsing capabilities or persistent storage. The REST API provides support for all authentication and authorization flows, but because it lacks a native SDK component. The SDKs provided and maintained by Adobe Primetime Authentication come with out-of-the box functionalities that implement business rules which in case of the REST API have to be implemented and maintained by the Programmers. In the Programmer Responsibilities table below we describe the limitations of the current REST API that need to be addressed by Programmers.

 

### Server-to-Server vs Client-based Pros and Cons

A Server-to-Server architecture provides a way to consolidate most of the authentication and authorization related logic into a single logical unit or implementation.  This approach has pros and cons.  The pros include:

* Single implementation for authentication and authorization business logic.
* Avoid the need to implement that logic on each supported platform using that platforms native tools.
* The ability to update capabilities without having to update clients with all their associated requirements (e.g. app store updates).
* **More easily** extend and custom authN and authZ capabilities (e.g. add D2C).
* Direct management of associated traffic for greater control, quality and monitoring.

 

Again, the cons are listed in the Programmer's responsibilities, but include the following:

* SSO must be implemented for each client for platforms without Platform SSO.
* Programmers must implement MVPD-specific logic if needed.
* All platforms using the REST API share a single configuration governing properties such as authentication TTLs.

 

### Connected Devices

For most connected devices, the REST API must be used in one way or another since an SDK is unavailable. The connected device will either use the REST API directly, or integrate with a Server-to-Server solution that uses the REST API.

## Programmer Responsibilities {#programmer-responsibilities}

The following apply to both Server-to-Server and Connected Device applications.

| **Functionality** | **Responsible for handling the functionality** | **Description of the limitations of current Clientless API and differences from native SDKs** |
| --- | --- | --- |
| Configuration settings applied per Platform | Adobe | One **major limitation** on using REST API throughout all platforms (including mobile devices like iOS & Android) is that the configuration settings corresponding to REST API in our TVE Dashboard configuration tool are applied across all devices (even if there is an iOS device that runs a native application implemented on top of our REST API). This limitation **can break** the agreed TTLs and agreed platform settings with the MVPDs - if those differ per each platform. [1](#1) |
| Single Sign-On | Programmers | Using the REST API, SSO is available only on platforms which support Platform SSO (e.g. Apple, Roku, Amazon) while SSO can not be guaranteed for other platforms when using the REST API. The SDKs cache data in a cross site/app way. This means the user logs in once on a site/app, and is already logged in on participating sites, without any user interaction needed. [2](#2) |
| Single Logout | Programmers | In a native SDK SSO scenario, logging out from one participating application will log out the user from everywhere. On the current REST API we don't support SLO, logging out from one application will log the user out only for that particular application. |
| Caching | Programmers | The REST API implementations will have to implement their own caching mechanism for business agreed data items. The SDKs are automatically caching various data items, while taking into consideration various business rules. For example the user metadata is cached with the same TTL as the authentication token, while some items can be programmatically excluded from caching (preflight). |
| Detailed Error Reporting mechanism | Programmers | The REST API primarily relies on HTTP error codes for reporting application errors while SDKs have a detailed error reporting mechanism that help the application developers to better understand what's happening. |
| Application error recovery (retry on error, loop detection etc.) | Programmers | REST API implementations need to build their own application recovery systems while implementations over on top of SDKs benefit from the SDKs error recovery system: recovery from transient network errors, by retrying certain network calls with in place logic to prevent "loops". |
| Authentication per requestor | Programmers | Some MVPDs require authentication for each site/app, either for business reasons, or due to technical challenges. The SDKs automatically enforce this based on TVE Dashboard configuration. The REST API implementers must implement this themselves, in order not to breach business agreements, or to be able to complete authorization for those MVPDs that scope their authentication data per application. |
| Passive authentication | Programmers | Some MVPDs support "passive" authentication, where the user is not required to enter the credentials, and an attempt to authenticate the user is made automatically. This is especially useful for MVPDs that also have "Authentication per requestor" as a requirement. For such a case, the UX enabled by the SDKs is seamless, where the user authenticates only once in an application, and the SDK performs "passive" authentication for other applications in the ecosystem. The user does not see the additional passive calls, he will simply be already authenticated, while the MVPD achieves the goal of having separate authentication sessions for each application. |
| Implicit and uniform device detection | Programmers | The SDKs automatically detect the device type and send that info in a standard way. REST API implementations are prone to sending different information, depending on the implementor, thus skewing/breaking business rules and statistics across sites. **Programmers need to make sure that they sent us correct device information** on each of their apps. For server to server implementations, the REST api does not correctly identify the IP address of the end user, unless additional steps are taken. The IP address is important in certain use cases like fraud prevention or HBA. |
| Tamper proof TempPass | Programmers | Enforcing TempPass is based on a stable device id. The SDKs use hardware info/fingerprinting techniques to identify the device and this mechanism is not public, and thus more secure and collision free. For REST API implentations, the Programmers need to implement their own algorithms for device identification/fingerprinting. |
| Device binding | Programmers | Tokens generated on a device with an application over SDK are not portable, making it hard for a malicious user to share his tokens and provide access to other users. This is based on the same device id mechanism as the "tamper proof TempPass". For REST API, the tokens stay in the cloud, which means that two devices with the same deviceIDs making the same calls will get the same responses/access. Programmers need to make sure that they have a robust, secure & collision free mechanism for generating/allocating deviceIDs. |
| Predictable, and certified set of features | Programmers | The existing set of features in each SDK is consistent, predictable and fully certified and tested. Some business requirements are enforced via the SDKs, making it risky for the programmer to breach contracts while using the REST API. While the REST API might be more flexible, Adobe guarantees that the SDK implementations enforces business decisions, and settings from TVE Dashboard. In the case of Clientless, each Programmer implements its own subset of the business rules that suites its applications at a given point in time. |


1. As part of our new One API initiative we plan to fix this limitation and to be able to apply rules per platform based on the device identification.

2. Adobe continues to work with all major platforms to implement Platform SSO that can be used with our REST API. Our One API initiative will offer SSO support between apps implemented using native SDKs & apps implemented using REST API.

## Minimum Device Requirements {#min_reqs}

In order to use the Primetime authentication REST API, devices must meet or exceed the minimum technical requirements listed in the REST API section of the [Primetime authentication Platform / Device / Tools Requirements document](#general_clientless_reqs).
