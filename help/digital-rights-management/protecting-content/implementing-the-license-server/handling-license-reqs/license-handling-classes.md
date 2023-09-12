---
title: Overview
description: Overview
copied-description: yes
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
---
# Overview {#overview}

To obtain a license, clients form a request from the metadata embedded in packaged content, then submit that request to the license server. The license server uses information extracted from the content metadata for generating a license.

If the client and server both support protocol version 5, the request URL is "License Server URL in metadata" + " [!DNL /flashaccess/license/v4]". If protocol version 3 is the maximum supported by either the client or server, Primetime DRM clients then send authentication requests to "License Server URL in metadata" + " [!DNL /flashaccess/license/v3]". Otherwise, authentication requests are send to "License Server URL in metadata" + " [!DNL /flashaccess/license/v1]"

A device may have multiple licenses for the same content (same License ID), but can only have one license for a particular License ID and DRM Policy ID. If it receives a license with a duplicate LicenseID/PolicyID, the new license then replaces the old one only if the new license's issue date is later than the existing license's issue date. This logic is used to process licenses embedded into content. Therefore it is not recommended to embed more than one license with the same DRM Policy ID in a chunk of content. The same logic applies to licenses passed to the client through the `DRMManager.storeVoucher()` ActionScript3 API; if the client already possesses a license with a later issue date, the provided license may be ignored.

## License request handling classes {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - This is the license request handler class. It reads and parses license requests. Its `getRequests()` method returns a list of `LicenseRequestMessage` objects. 
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - This is the request message class. The caller should iterate through the `LicenseRequestMessage` list returned by `getRequests()`, and for each request either generate a license or set an error code. Call `LicenseRequestMessage.getContentInfo()` to obtain information extracted from the content metadata, including the content ID, license ID, and DRM policies.

Licenses and errors are sent at one time when the `LicenseHandler.close()` method is called.

See the [DRM Server API reference documentation](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) for details.
