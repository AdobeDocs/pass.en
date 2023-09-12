---
title: Block list of DRM Clients restricted from accessing protected content
description: Block list of DRM Clients restricted from accessing protected content
copied-description: yes
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
---
# Block list of DRM Clients restricted from accessing protected content {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Access DRM module versions restricted from accessing protected content.**

Specifies the DRM client that cannot access content. Specified by DRM client version and platform.

Example use case: In the event of a security breach, a newer version of the DRM client can be specified as the minimum version required for license acquisition and content playback. The license server checks that the DRM client making the license request meets the version requirements before issuing a license. The DRM client also checks the DRM version in the license before playing content. This client check is required in the case of domains where a license may be transferred to another machine.

A DRM client version may be identified by the attributes specified in the following table: 

| **Attribute** |**Supported Values** |**Match Criteria** |**Description** |
|---|---|---|---|
|  Environment  | “PC”, “PortingKit”  | Exact Match  | Identifies whether the client is running on a Desktop or any other device.  |
|  OS  | “Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"  | Exact Match  | Platform  |
|  Architecture  | “32”, “64”  | Exact Match  | 32-bit or 64-bit  |
|  Screen Type  | “PC”, “Mobile”, “TV”  | Exact Match  | |
|  Runtime Version  | A valid version number. For instance, “2.0.0”, "3.0", "4.0", "11.0", etc.  | Matches if client version is less than or equal to the specified version.  | Version number is specified as a combination of numbers and periods (“.”) of any length.  |
|  DRM Library Version  | A valid version number. For instance, “2.0.0”.  | Matches if client version is less than or equal to the specified version.  | Version number is specified as a combination of numbers and periods (“.”) of any length.  |
|  OEM Vendor  | OEM Vendor string  | Exact Match  | OEM Vendor identification string for the device using the porting kit.  |
|  Model  | Model string. For example, "iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"  | Exact Match  | Device model identification string for the device using the porting kit.  |

>[!NOTE]
>
>When specifying an entry in the block list, values may be set for one or more of the attributes mentioned in the previous table. Any attribute that is not specified is treated as a wildcard. If the DRM client matches all the values specified in a block list entry, protected content may not be accessed by that client.
