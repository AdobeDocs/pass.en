---
title: Cookies Updates - SameSite and Secure flags
description: Cookies Updates - SameSite and Secure flags
exl-id: cc1f60fd-fa64-48cb-a185-dba562a54c33
---
# (Legacy) Cookies Updates - SameSite and Secure flags {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>


## Updates {#Updates}

This section highlights the changes introduced by Chrome browser and Adobe Pass Authentication for handling 3rd party cookies.

 

### Chrome 80 Updates {#Chrome}

Starting with Chrome version 80 (except version 82), cookies that do not specify a *SameSite* attribute will be treated as if they were *SameSite=Lax*. Therefore, cookies that need to be delivered in a cross-site context must explicitly specify the *SameSite=None*, and must also be marked with the *Secure* attribute and delivered over *HTTPS*. More details about these updates can be read from the official chromium page: <https://www.chromium.org/updates/same-site> and also from <https://web.dev/samesite-cookies-explained/>.


### Adobe Pass Authentication Updates {#Pass-Updates}

Adobe Pass Authentication service is currently relying on a couple of cookies which are considered third party cookies from the browser's point of view, including Chrome, in order to function in combination with some platforms and versions of Adobe Pass Authentication SDKs. Therefore, in order to comply with the upcoming changes and continue to deliver these cookies in a cross-site context from these older SDKs, Adobe Pass Authentication service implements the required changes in the *adobe-pass-2.55.1* version.

These changes from the *adobe-pass-2.55.1* version involve adding the *Secure* and *SameSite=None* attributes for all its cookies passed back to all Adobe Pass Authentication SDKs when using Chrome browsers starting with version 80 and above (except version 82).

The next section presents some potential issues for a list of platforms and Adobe Pass Authentication SDKs versions in case one user is using Chrome browser 80 and above (except version 82).

## Troubleshooting {#Troubleshooting}

While browsing througth this section keep in mind that all Adobe Pass Authentication service cookies must have *Secure* attribute set in *adobe-pass-2.55.1* version for all browsers, while the *SameSite=None* attribute must be set only for Chrome browsers version 80 and above (except version 82).


### General Troubleshooting {#General}

1.  Important to note that some user agents are known to be incompatible with the *SameSite=None* attribute.

    - Versions of Chrome from Chrome 51 to Chrome 66 (inclusive on both ends). These Chrome versions will reject a cookie with *SameSite=None*. This also affects older versions of Chromium-derived browsers, as well as Android WebView. This behavior was correct according to the version of the cookie specification at that time, but with the addition of the new "None" value to the specification, this behavior has been updated in Chrome 67 and newer. (Prior to Chrome 51, the SameSite attribute was ignored entirely and all cookies were treated as if they were *SameSite=None*.)
    - Versions of UC Browser on Android prior to version 12.13.2. Older versions will reject a cookie with *SameSite=None*. This behavior was correct according to the version of the cookie specification at that time, but with the addition of the new "None" value to the specification, this behavior has been updated in newer versions of UC Browser.
    - Versions of Safari and embedded browsers on MacOS 10.14 and all browsers on iOS 12. These versions will erroneously treat cookies marked with *SameSite=None* as if they were marked *SameSite=Strict*. This bug has been fixed on newer versions of iOS and MacOS.


1. Important to note that cookies having the *Secure* attribute must be sent over *HTTPS*, otherwise the cookie will not reach the Adobe Pass Authentication service.

    - AccessEnabler JavaScript SDK:
        - Mandatory that the communication with *sp.auth.adobe.com* uses *HTTPS* for versions *2.35* and *3.5.0*, before introducing Dynamic Client Registration.
    - AccessEnabler iOS/tvOS SDK:
        - Mandatory that the communication with *sp.auth.adobe.com* uses *HTTPS* for versions prior to *3.0.0*, before introducing Dynamic Client Registration.
    - AccessEnabler Android SDK:
        - Mandatory that the communication with *sp.auth.adobe.com* uses *HTTPS* for versions prior to *3.0.0*, before introducing Dynamic Client Registration.
    - AccessEnabler FireOS SDK:
        - Mandatory that the communication with *sp.auth.adobe.com* uses *HTTPS* for version *2.0.4*.

</br>

### AccessEnabler JavaScript SDK version 2.35 Troubleshooting {#235-Troubleshooting}

User's authentication flow could be affected in Chrome 80 and above (except version 82). In order to make sure the user is not having troubles to authenticate because of the above updates one can:

- Check that the *JSESSIONID* cookie is set in browser and having the *SameSite=None* and *Secure* attributes set. 
- Check that the *JSESSIONID* cookie from the *https://sp.auth.adobe.com/authenticate/saml* network request matches the *JSESSIONID* cookie from the *https://sp.auth.adobe.com/session* network request.


### AccessEnabler JavaScript SDK version 3.5.0 Troubleshooting {#350-Troubleshooting}

User's authentication flow could be affected in Chrome 80 and above (except version 82). In order to make sure the user is not having troubles to authenticate because of the above updates one can:

- Check that the *JSESSIONID* cookie is set in browser and having the *SameSite=None* and *Secure* attributes set. 
- Check that the *JSESSIONID* cookie from the *https://sp.auth.adobe.com/authenticate/saml* network request matches the *JSESSIONID* cookie from the *https://sp.auth.adobe.com/session* network request.
- Check that the *pass\_sfp* cookie is set in browser and having the *SameSite=None* and *Secure* attributes set.
- Check that the *pass\_sfp* cookie is set in *https://sp.auth.adobe.com/session* network request.


User's authorization flow could be affected in Chrome 80 and above (except version 82). In order to make sure the user is not having troubles to watch a protected resource, after being successfully authenticated,  because of the above updates one can:

- Check that the *pass\_sfp* cookie is set in browser and having the *SameSite=None* and *Secure* attributes set.
- Check that the *pass\_sfp* cookie is set in *https://sp.auth.adobe.com/adobe-services/authorize* network request.
- Check that the *pass\_sfp* cookie is set in *https://sp.auth.adobe.com/adobe-services/shortAuthorize* network request.
