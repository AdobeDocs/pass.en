---
title: Amazon fireTV SSO - Programmer kick-off guide
description: Amazon fireTV SSO - Programmer kick-off guide
exl-id: cf9ba614-57ad-46c3-b154-34204b38742d
---
# Amazon fireTV SSO - Programmer kick-off guide {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#intro}

This document describes the information needed to integrate the new **Adobe Pass authentication's fireTV SDK** in your fireTV application. This new SDK takes advantage of OS level integration on Amazon's fireTV platform thus offering **Single Sign On** support. To benefit from Single Sign On there is a little effort required from your side in order to migrate your application from Clientless API to the new fireTV SDK. There are some changes in the authentication flows that will be detailed below.

## High level architecture and OS level integration {#high}

In order to achieve Single Sign On between TV Everywhere applications on Amazon fireTV platform and to improve the overall experience on this platform we decided to integrate our core SDK at fireTV OS level. Programmers will be required to compile against a stub library provided by Adobe. The actual functionality will be provided by Adobe's library present in Amazon's fireTV OS.

Until Amazon provides a fireTV simulator that incorporates our library at OS level the development would be possible only using real fireTV devices.

## Benefits {#bene}

* Single Sign On between all Adobe powered TV Everywhere applications on Amazon fireTV platform with all integrated MVPDs.
* Ability to benefit from HBA (with supported MVPDs).
* Ability to use the latest fireTV SDK without the need to update your applications each time a new SDK version is released.
* All TVE apps benefit from using the shared system library by removing the need of having a local copy of AccessEnabler library. This also makes sure that all applications are using the same SDK version.
* Single screen authentication - no need of registration code & 2nd screen workflows.

## Migration from Clientless API based app to fireTV SDK based app {#migra1}

For migrating from Clientless API to fireTV SDK you need to remove the codebase related to the Clientless API and to integrate the new fireTV SDK.

Compared with Clientless API based app, with the new fireTV SDK the authentication moves to first screen, there is no need for a second screen authentication anymore.

This requires Programmers to add an MVPD picker into their apps so that users can pick their TV provider right on the fireTV device. Upon MVPD selection the user will be shown the MVPD login page on the fireTV device.

Wireframes of the user flows that describe the regular, HBA, and SSO scenarios on fireTV can be found at [Amazon Fire TV - MVVPD Sign-in User Flow](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## Migration from Android SDK based app to fireTV SDK based app {#migra2}

This new fireTV SDK is very similar to our existing Android SDK and the current documentation we have for **integrating our Android SDK** <!--http://tve.helpdocsonline.com/android-technical-overview-->can be used until we have the fireTV SDK documents ready. If you already have Android applications that use our Android SDK then the integration of fireTV SDK in your fireTV application should be straightforward.

Compared with existing Android SDK, on fireTV SDK the authentication process will be simpler to develop since the tasks of managing / presenting the MVPD login page and retrieving the AuthN token will be performed internally by AccessEnabler library.

## FAQs {#faq}

1.  How will the **SSO** work?
    
      * SSO will work across all Programmer applications powered by Adobe Pass authentication that are using the new fireTV SDK on the same Amazon fireTV device
      * SSO between Programmer apps implemented on Clientless REST API and apps implemented on fireTV SDK **will NOT be supported**

1.  What is the MVPD coverage of fireTV SSO?
    
      * **All MVPDs** integrated by Adobe Pass authentication will be technically SSO supported on fireTV SDK.

1.  Besides using the new SDK, what other **workflow changes** should Programmers be aware of?
    
      * Programmers need to implement a MVPD picker for fireTV platform.

1.  Will there be any change to the authentication **TTLs**?
    
      * There is no change in behavior regarding authentication TTLs.
      * The first valid authentication token will be used for performing the SSO and in this case all the other applications that will be authenticated through SSO will use the same TTL until it expires. So when navigating from one application to another, the second application will share the TTL of the first application that authenticates.

1.  How the **degradation API** work?
    
      * There are no changes needed for degradation API, the user experience will be the same as on Android devices.

1.  How **TempPass** flows are affected?
    
      * TempPass flows are single screen and behave as on any other native devices.

1.  Will other Adobe functionality work as before?
    
      * All Adobe Pass authentication functionality will work on fireTV as on Android devices.
