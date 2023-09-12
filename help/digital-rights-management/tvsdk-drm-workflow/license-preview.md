---
title: License preview
description: License preview
copied-description: yes
exl-id: 53a57610-86a8-4c5d-9494-679ede35abf8
---
# License preview {#license-preview}

If there is a question around whether or not a device can consume and fully enforce a Primetime DRM license, you can use the License Preview feature. A Preview license fully matches all constraints and restrictions defined in the final license, but does not contain the Content Encryption Key (CEK) needed to decrypt the protected content. This capability is useful to determine whether the client can indeed consume the license before the Content Distributor makes a decision to provide a particular license to the client. For example - a customer wishes to watch HD content, but the Content Distributor wants to ensure that the device can fully detect and engage HDCP. In this situation, the client can call `DRMManager.loadPreviewVoucher()`. If a `DRMStatusEvent` is received, instead of a `DRMErrorEvent`, then it is confirmed that the client can fully enforce the Output Protection restrictions in the license, and the Content Distributor can freely provide this type of license to the client.

[iOS acquirePreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquirePreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
