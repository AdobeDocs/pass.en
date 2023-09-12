---
title: Roku SSO overview
description: About Roku SSO
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
---
# Roku SSO Overview {#overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#roku-sso-intro}

This document describes the information needed to take advantage of Single Sign On capability on Roku devices. Adobe Primetime Authentication collaborates with Roku to improve the login user experience and to facilitate Single Sign On across TV Everywhere applications for TV subscribers. 

The solution is based on the Adobe Primetime authentication's Clientless REST API, so most Programmers won't need to update their applications to benefit from Single Sign On.

## Enabling Roku SSO {#enable-roku-sso}

Roku SSO is enabled by default unless the Programmer or MVPD request for SSO to be disabled.

Each Programmer can Enable / Disable SSO on the Roku platform for specific integrations.

### What a Programmer should do for Roku SSO to work {#make-roku-sso-work}

For Programmers' applications implementing REST API on client devices, the Roku SSO will work without any change. Roku OS will add two HTTP headers on any request to Adobe Primetime Authentication end-points. 

For Programmers' applications implementing a Server to Server solution for REST api , the Programmer should contact the Roku team and ask for a configuration where these two headers will be sent to their domain on all api flows. 

Roku-provided subscriber ID to be used instead of whatever device ID is passed by the application to ensure cross-application (and cross-device) SSO. 

For specific details about the format of the needed headers, please contact your Adobe representative. 

### Possible issues {#possible-issues}

Programmers should check that their current implementations based on Adobe's Clientless REST API don't impede Roku's platform-SSO. See below a list of possible issues and how they should be solved.

| Problem | Possible cause | Possible solutions |
|-|-|-|
|No Roku SSO header sent to Adobe|Using HTTP instead of HTTPS for calls to Adobe Primetime authentication domains|Use HTTPS|
|MVPD logo not shown / not updated for SSO tokens|UI relies on local storage|Applications should update UI (and local storage, if needed) after checking authentication|
|Logout triggered on no AuthZ|Application design|Application should be updated to never perform logout behind the scenes|

## FAQ {#faq}

* **How will the SSO work?**

  SSO will work across all Programmer applications powered by Adobe Primetime authentication on all Roku devices associated with the same Roku user.
Not all MVPDs will allow Roku SSO. 

* **Will there be any change to the authentication TTLs?**

  The first valid authentication token will be used for performing SSO and, in this case, all the other applications that will be authenticated through SSO will use the same TTL until it expires. So, when navigating from one application to another, the second application will share the TTL of the first application that authenticates.

* **Will other Adobe functionality work as before?**

  All Primetime authentication functionality will work as before.

* **Is there a Programmer opt-in / opt-out process benefiting from SSO on the Roku platform?**

  This will be a configuration change in Adobe's TVE Dashboard. Each Programmer can Enable / Disable SSO on the Roku platform for specific integrations.
