---
title: Play Rights
description: Play Rights
copied-description: yes
exl-id: a4fda537-dbcc-496b-8f15-c13b25fe87b0
---
# Play Rights {#play-rights}

The following table describes the Play Rights preferences: 

| Preference | Description |
|--- |--- |
|Playback Window|The duration a license is valid (in minutes) after the first time the user plays the protected content.|
|Output Protection|Controls whether output to external rendering devices should be protected. Analog and digital outputs can be specified independently.|
|Restrictions|Block list of client versions not permitted to play content. All columns are optional.|
|DRM|Specifies a list of DRM versions that are not permitted to play protected content.|
|Runtime|Specifies a list of Runtime versions that are not permitted to play protected content.|
|Minimum Security Level||
|DRM|Minimum DRM security level required to play protected content.|
|Runtime|Minimum Runtime security level required to play protected content.|
|Allowed Applications|Allow list of client applications permitted to play content. If not applications are specified, any SWF or AIR application is allowed.|
|SWF|List of SWF URLs permitted to play protected content.|
|AIR|List of AIR applications permitted to play protected content. Publisher ID is required, the remaining fields are optional.|

Flash Access Manager supports policies containing multiple Play Rights. To create a policy with more than one Play Right, use the "Add additional Play Right" button, and fill in the desired attributes for each Play Right.

When consuming a license, the client uses the first Play Right for which it meets all the requirements. Multiple play rights may be used to specify different restrictions for different operating systems. For example, it is possible to specify one right with Output Protection required for Windows (by block listing DRM versions on Macintosh and Linux) and to specify a second right with Output Protection "Use if available" on other platforms (by block listing DRM versions on Windows).
