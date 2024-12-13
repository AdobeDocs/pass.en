---
title: Tracking Prevention Assessment Apple Safari
description: Tracking Prevention Assessment Apple Safari
exl-id: a3362020-92ff-4232-b923-e462868730d5
---
# (Legacy) Tracking Prevention Assessment - Apple Safari {#tracking-prevention-assessment-apple-safari}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Safari 10 {#safari10}

**Details**

Starting with Safari 10, the default browser privacy settings will cause the Single Sign-On (SSO), Single Logout (SLO) and passive authentication features to stop working. The Single Sign-On (SSO) and passive authentication will not work even in
the same session between multiple tabs or browser windows.

These changes affects and are having an impact on Adobe Pass Authentication processes
for the following versions of the AccessEnabler JavaScript SDK: v2 (versions 2.x), v3 (versions 3.x), v4 (versions 4.x).

### Mitigation {#mitigation-safari10}

In order to mitigate these limitations you can instruct the user to change the Safari 10 browser privacy settings, and use the "**Always allow**" option for the "**Cookies and website data**" entry in the browser's Privacy tab from Preferences, as depicted in bellow image.

![](../../../assets/always-allow-safari10.png) 


## Safari 11 {#safari11}

**Details**

>[!IMPORTANT] 
>
>All above details from section Safari 10 still apply in case of Safari 11.

Starting with Safari 11, the browser introduces [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP) mechanism, a technology that uses heuristics in order to prevent cross-site tracking. These heuristics impact the way 3rd party cookies are stored and replayed on network calls, meaning that depending on the ITP mechanism activation the Safari browser will block 3rd party cookies in the client - server model communication.  

Adobe Pass Authentication service uses and relies on cookies as part of the authentication process **in order to function**. In situations where the authentication process takes place automatically (e.g. Temp Pass) or in implementations that use iFrames or "refressless" functionality, Adobe's cookies are considered 3rd party cookies and blocked by default. For any other cases, Safari uses a machine learning algorithm that might flag all Adobe's Pass Authentication service cookies as tracking cookies, therefore being subject for ITP's blocking.  

In conclusion, a user of Safari 11 browser might be unable to authenticate on an Adobe Pass Authentication enabled website after the activation of the Intelligent Tracking Prevention (ITP) mechanism, especially when the user is using multiple Adobe Pass Authentication enabled websites. Therefore, the user's authentication experience might be unexpected and undefined, ranging from inability to log in, to shorter than expected authentication duration.

These changes affects and are having an impact on Adobe Pass Authentication processes fo the following versions of the AccessEnabler JavaScript SDK: v2 (versions 2.x), v3 (versions 3.x).

### Mitigation {#mitigation-safari11}

For both AccessEnabler JavaScript SDK v3 (versions 3.x) and AccessEnabler JavaScript SDK v4 (versions 4.x), the library contains a mechanism capable to identify the situations where user's authentication was blocked due to missing required cookies. In these situations the library triggers a specific error callback [N130](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md#advanced-error-codes-reference), which is passed back to the Adobe Pass Authentication enabled website in order to be used as a signal to instruct the user to take actions which can mitigate the issue. In order to benefit from this mechanism the website must implement the [Error Reporting](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) specification.

For AccessEnabler JavaScript SDK v2 (versions 2.x), the library does not offer the above described mechanism, therefore the Adobe Pass Authentication enabled website can not be signaled when to instruct the user to take actions to mitigate the issue.  

The list of actions which can mitigate the aforementioned issues **applies for all three versions** of AccessEnabler JavaScript SDK. 

When [N130](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md#advanced-error-codes-reference) error callback is received by the implementor's website, the user should be instructed to disable Intelligent Tracking Prevention (ITP) and enble 3rd party cookies by:

* In case of Mac OS X High Sierra and later: Unchecking the "**Prevent cross-site tracking**" option for "**Website tracking**" entry in the browser's Privacy tab from Preferences, as depicted in bellow image.

  ![](../../../assets/uncheck-prvnt-cr-st-tr-safari11.png)


* In case of Mac OS X Sierra and previous: Checking the "**Always allow**" option for the "**Cookies and website data**" entry in the browser's Privacy tab from Preferences, as depicted in bellow image. 

  ![](../../../assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**Details**

>[!IMPORTANT] 
>
>All above details from section Safari 10 and section Safari 11 still apply in case of Safari 12.

This section details the compatibility issues of **AccessEnabler JavaScript SDK versions 4.x** on Safari 12.

>[!NOTE] 
>
>Bear in mind that in case of AccessEnabler JavaScript SDK versions 2.x and AccessEnabler JavaScript SDK versions 3.x, they both use 3rd party cookies for the authentication processes, and due to ITP and 3rd party cookies policies starting with Safari 11, user's authentication experience might be unexpected and undefined, ranging from inability to log in, to shorter than expected authentication duration.


### Certified functionality of AccessEnabler JavaScript SDK v4 (versions 4.x) on Safari 12 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

**Authentication** flows that make use of user interaction will always work, even if the user's browser have 3rd party cookies disabled, because starting with version 4.0 the AccessEnabler JavaScript SDK does not use 3rd party cookies anymore for the authentication processes.

>[!NOTE] 
>
>The user MUST interact with the site in order to open login popups and/or interact with the MVPD login page.

**Authorization/Preflight/User Metadata** operations are fully functional, provided the user is already authenticated.

### Known issues of AccessEnabler JavaScript SDK v4 (versions 4.x) on Safari 12 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO and SLO

  * Due to how the localStorage is implemented in Safari starting from Safari 10, the JS SDK cannot share the login state anymore via a common domain iFrame. This means that the user needs to log in on every site that uses AccessEnabler JavaScript SDK. Logging out also does not delete authentication tokens across sites, therefore the user needs to log out from each Adobe Pass Authentication enabled website.

* Temp Pass

  * For temporary passes, the AccessEnabler JavaScript SDK uses an individualization mechanism, in order to lock an authentication token to a specific device (browser instance). Due to new mechanisms in Safari 12 designed to prevent tracking, the fingerprint we are computing and using in the individualization mechanism **will be the same for all users that have the same IP address**. We do take the client IP in consideration for individualization purposes, but even so the impact is on users that share the same public IP address. For these users, we will compute the same individualization id, and the temporary pass will be  tied to it. This means that once such a user uses a temporary pass, nobody else will have access to it \! This impacts especially corporate users, education institutions, or any other organization that have multiple users using NAT or a common proxy to access the internet.

>[!NOTE] 
>
>This issue is affecting users only if the implementor uses Temp Pass as a result of user interaction, otherwise Temp Pass authentication is subject to **Automatic flows** below.

* Automatic flows

  * Authentication flows attempted in an automated mode, without any user interaction will not succeed in Safari 12 when using JS SDK 4.0. Note that the upcoming JS SDK 4.1 fixes all issues with automated flows.

Use cases affected by this issue:

* Automatic TempPass (Free Preview) authentication - for such flows, the SDK will throw an N130 error.

* Passive Authentication (fails silently) – user is asked to select this MVPD and enter credentials

### Mitigation {#mitigation-safari12}

**SSO and SLO**

There is no known mitigation available or possible at the moment of these writing. Apple did introduce an "Storage Access API" in Safari 12 (`https://webkit.org/blog/8124/introducing-storage-access-api`), but the current implementation does not apply to localStorage but only to cookies. Moreover the API requires user interaction in order to be used, and once you use it, the user is also prompted with a permission dialog similar with the one below.

![](../../../assets/permission-dialog-apple.png)

  
At this point these Safari requirements/prompts do not align with our UX requirements and we don't have a consistent behavior as on other browsers, where SSO "just works" once we saved a token in a common domain localStorage.

**Temp Pass**

In order to mitigate the individualization problems and to have a user interaction we recommend you to use **[Promotional Temp Pass ](/help/authentication/integration-guide-programmers/features-premium/temporary-access/promotional-temp-pass.md)** n a interactive way, and provide at least one additional information about the user (for example, email address).

## Safari 13 {#safari13}

**Details**

>[!IMPORTANT] 
>
>All above details from section Safari 10 up to section Safari 12 still apply in case of Safari 13.


Starting with Safari 13, the browser introduces new changes to the [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP), making the heuristics behind the mechanism stricter in the process of flagging 3rd party cookies as tracking cookies, in order to prevent cross-site tracking.

As described in previous sections Adobe Pass Authentication service uses and relies on 3rd party cookies as part of the authentication processes when implementors are using the AccessEnabler JavaScript SDK v2 (versions 2.x) and  AccessEnabler JavaScript SDK v3 (versions 3.x). Compared to previous versions of Safari browser when ITP was kicking in after spending a while to "learn" about the interaction between the user and the involved parties (programmer's websites and Adobe), the Safari 13 browser is blocking from the start 3rd party cookies which are considered tracking cookies in the client - server model communication.

In conclusion, a user of Safari 13 browser will most probably be unable to initiate new authentications on an Adobe Pass Authentication enabled website which is using an older version of AccessEnabler JavaScript SDK, v2 (versions 2.x) or v3 (versions 3.x). This is happening due to the fact that all required Adobe's Primetime Authentication service cookies are blocked by ITP, therefore making the service unable to fulfil the authentication request.

AccessEnabler JavaScript SDK v4 (versions 4.x) library does not use 3rd party cookies for the authentication process, therefore its operations are not affected in any way by the Safari 13 changes.

### Mitigation {#mitigation-safari13}

First and foremost we are strongly recommending **migration to AccessEnabler JavaScript SDK versions 4.x** to have a stable and predictable behavior on Safari browser.

Secondly, for AccessEnabler JavaScript SDK v3 (versions 3.x), the library contains a mechanism capable to identify the situations where users authentication was blocked due to missing required cookies. In these situations the library triggers a specific error callback ([N130](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md#advanced-error-codes-reference)) which is passed back to the Adobe Pass Authentication enabled website in order to be used as a signal to instruct the user to take actions which can mitigate the issue. In order to benefit from this mechanism the website must implement the [Error Reporting](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md) specification.

For AccessEnabler JavaScript SDK v2 (versions 2.x), the library does not offer the above described mechanism, therefore the Adobe Pass Authentication enabled website can not be signaled when to instruct the user to take actions to mitigate the issue.

When [N130](/help/authentication/integration-guide-programmers/legacy/error-reporting/error-reporting.md#advanced-error-codes-reference) error callback is received by the implementor's website, the user should be instructed to disable Intelligent Tracking Prevention (ITP) and enble 3rd party cookies by:

* In case of Mac OS X High Sierra and later: Unchecking the "**Prevent cross-site tracking**" option for "**Website tracking**" entry in the browser's Privacy tab from Preferences, as depicted in bellow image.

  ![](../../../assets/prvnt-cross-site-tr-safari13.png)

* In case of Mac OS X Sierra and previous: Checking t</span>he "**Always allow**" option for the "**Cookies and website data**" entry in the browser's Privacy tab from Preferences, as depicted in bellow image.

  ![](../../../assets/always-allow-safari13.png)
