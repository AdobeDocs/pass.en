---
title: Non-SWF Application Allow listing
description: Non-SWF Application Allow listing
copied-description: yes
exl-id: f33fb0e9-144f-49f8-8da2-8a50aea09456
---
# Non-SWF Application Allow listing {#non-swf-application-isting}

AIR was the first platform that featured application allow listing, and the name of the property you use to allow list non-SWF applications (Adobe AIR, iOS, Android, etc.) retains its original name: `policy.allowedAIRApplication.n`. This allows the content to be played back by all non-Flash applications that are signed with a Signing Certificate prior to publishing. This is referred to as the *Application ID*. You can extract the Application ID by using the [!DNL AdobePublisherIDUtility.jar] tool. This allow listing will be enforced on any client that supports Primetime DRM.

The Application ID is derived from the public key of the signing certificate used to sign a particular application. If the public key in the certificate ever expires, then all previous content allow listed to only play on apps signed with the old certificate will not play on the new app (signed with the new certificate).

If you are in the situation where you have a library of content allow listed to applications that were signed with a particular signing certificate, and that certificate expires and you are issued a new certificate (with a different public/private keypair), your old content will not play on your new app *unless* you do any of the following:

* Use a `PolicyUpdateList` on your license server to override the incoming policy and insert a new Application Allow list entry with your new signing certificate's digest . 
* Update your license server's logic to override the incoming policy and insert a new Application Allow list entry. 
* Request that your signing certificate issuer issues you a new certificate that uses the same public/private keypair that your previous certificate used. 
* If you are delivering HDS/HLS content that is referencing a URL endpoint to retrieve the `DRMMetadata`, you can regenerate the `DRMMetadata` (using the Primetime DRM Java SDK) to insert a new DRM Policy that contains an updated Application Allow list entry. 

* Repackage all of your old content with a new DRM policy that has the digest of your new signing certificate.

See `policy.allowedAIRApplication.n` in *Configuration properties* for details.

>[!NOTE]
>
>Allow listing an iOS application requires you a special approach. See [Allow list your iOS application](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) in the *TVSDK for iOS Programmer's Guide*.
