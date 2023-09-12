---
description: With the Adobe Primetime DRM Server for Protected Streaming, you can specify all usage rules on the server with configuration files.
title: About usage rules
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
---
# About usage rules{#about-usage-rules}

With the Adobe Primetime DRM Server for Protected Streaming, you can specify all usage rules on the server with configuration files.

Any usage rules specified in the DRM policy for the protected content are overridden. Therefore Adobe recommends that you use a simple, anonymous DRM policy during content packaging. Any usage rules that you can configure can be configured on a per-tenant basis.

The Primetime DRM Server for Protected Streaming supports the following usage rules:

* Output Protection 
* Adobe® AIR®, SWF, iOS, and Android Application Restrictions 
* DRM and Runtime Module Restrictions 
* Jailbreak detection enforcement on Primetime DRM platforms that support jailbreak detection 
* License Caching is disabled by default. License caching that you can enable by specifying the caching end date or an amount of time caching is allowed; it starts when the license is issued. 
* Multiple Play Rights that let you specify different combinations of Output Protection, Application Restrictions, and DRM/Runtime Restrictions. For example, you can specify different Output Protection requirements for each client platform by using the DRM Module Restriction with Output Protection.

>[!NOTE]
>
>If you want to support remote key delivery to iOS devices, then the DRM policy that is applied at packaging time must have remote key delivery enabled. This setting cannot be modified through the tenant configuration on the server.
