---
description: Common problems during testing often involve your ExpressPlay authenticators, transport protocols, and required service request parameters.
title: Troubleshooting your quick-start
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
---
# Troubleshooting your quick-start{#troubleshooting-your-quick-start}

Common problems during testing often involve your ExpressPlay authenticators, transport protocols, and required service request parameters.

If your [!DNL curl] requests to ExpressPlay for token generation fail, the response body will contain an error message that explains the reason for failure.

If the token generation is successful, but the content still does not play, check the ExpressPlay token redemption logs for errors such as "Expired token".

If the token generation was successful and redemption had no error, but the video still does not play, check that the CEK matches the content, and that the content format matches the capabilities of the target device.

In addition:

* Check that you are using the correct Customer Authenticator in your service requests. It is easy to accidentally use the production authenticator when you meant to use the test authenticator. Also, make sure you are using *your* authenticator. For example, during testing you might borrow somebody else's `curl` command and forget to swap in your authenticator for theirs. 

* Check that you are using the proper transport protocol in your requests or in your manifests ( `https://` versus `https://`, or in the case of FairPlay, `skd://` versus `https://` versus `https://`. 

* Make sure that you are including all of the required query parameters for the DRM solution you are working with. It is easy to get confused between PlayReady and Widevine for instance, because they are both working with DASH, but the required request parameters and packaging configurations are different. 
* Confirm that your ExpressPlay account has enough token credits and has not been exhausted. 
* Confirm that the triplet of DRM data being sent to the TVSDK is correct: ExpressPlay token, license server URL, and DRM type. 
* Confirm that all of your components are making the same assumption about which ExpressPlay environment is in use as there are two environments, Test and Production. 
* Be aware that different browsers typically support only one DRM for DASH content. 
* As of TVSDK 2.4, only the DASH-LIVE packaging profile is supported. (DASH-OnDemand support is on the roadmap.) 
* AndroidTV PlayReady support is intermittent due to device manufacturer limitations. To give examples,

    * the Razer Forge device has issues with PlayReady content 
    * Amazon FireTV cannot consume DASH content that has the audio track encrypted

* As of TVSDK 2.4, only AndroidTV devices typically support both PlayReady and Widevine DRMs. All other Android devices typically only support Widevine. 
* As of TVSDK 2.4, the Android TVSDK currently requires that the PSSH box is in the .mpd manifest. This is contrary to the DASH standard, which specifies that the PSSH box can be anywhere, like in the content itself, and not just in the .mpd.
