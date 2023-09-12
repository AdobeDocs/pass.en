---
title: Block list of DRM Clients restricted from accessing protected content
description: Block list of DRM Clients restricted from accessing protected content
copied-description: yes
exl-id: 837e55ef-8dff-46eb-a952-c787d40d4a1b
---
# Block list of DRM Clients restricted from accessing protected content {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

This block list specifies the Primetime DRM clients that cannot access protected content. You block list clients by client version and platform.

Example use case: In the event of a security breach, a newer version of the Primetime DRM client can be specified as the minimum version required for license acquisition and content playback. The license server checks that the Primetime DRM client making the license request meets the version requirements before issuing a license. The Primetime DRM client also checks the version in the license before playing content. This client check is required in the case of domains where a license may be transferred to another machine.

A Primetime DRM client version may be identified by the attributes specified in the following table: 

| **Attribute** |**Supported Values** |**Match Criteria** |**Description** |
|---|---|---|---|
|  Environment  | `“PC”, “PortingKit”`  | Exact Match  | Identifies whether the client is running on a Desktop or any other device.  |
|  OS  | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"`  | Exact Match  | Platform  |
|  Architecture  | `“32”, “64”`  | Exact Match  | 32-bit or 64-bit  |
|  Screen Type  | `“PC”, “Mobile”, “TV”`  | Exact Match  | |
|  Runtime Version  |A valid version number. For instance, `“2.0.0”, "3.0", "4.0", "11.0"`, etc.  | Matches if client version is less than or equal to the specified version.  | Version number is specified as a combination of numbers and periods (“.”) of any length.  |
|  Primetime DRM Library Version  |A valid version number. For instance, `“2.0.0”`.  | Matches if client version is less than or equal to the specified version.  | Version number is specified as a combination of numbers and periods (“.”) of any length.  |
|  OEM Vendor  | OEM Vendor string that can be located in the Runtime Certificate that was issued to a customer who ported Primetime DRM to a device.  | Exact Match  | OEM Vendor identification string for the device using the porting kit.  |
|  Model  |Model string that can be located in the Runtime Certificate that was issued to a customer who ported Primetime DRM to a device. For example, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"`  | Exact Match  | Device model identification string for the device using the porting kit.  |

>[!NOTE]
>
>When specifying an entry in the block list, you can set values for one or more of the attributes mentioned in the previous table. Any attribute that is not specified is treated as a wildcard. If the Primetime DRM client matches all the values specified in a block list entry, protected content may not be accessed by that client.
