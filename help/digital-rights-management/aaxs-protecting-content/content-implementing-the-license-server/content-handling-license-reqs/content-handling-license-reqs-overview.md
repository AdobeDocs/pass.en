---
title: Overview
description: Overview
copied-description: yes
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
---
# Overview{#overview}

To request a license, the client sends the metadata that was embedded in the content during packaging. The license server uses the information in the content metadata to generate a license.

The `LicenseHandler` reads a license request and parses the request. `LicenseHandler`extends `BatchHandlerBase` to accommodate batch license requests, although this feature is not currently supported by Adobe Access clients. The `getRequests()` method will return a List of `LicenseRequestMessage` objects. The caller should iterate through the `LicenseRequestMessages`, and for each request, either generate a license or set an error code (see the `LicenseRequestMessage` API reference documentation for details). For each license request, the server determines whether it will issue a license. Call `LicenseRequestMessage.getContentInfo()` to obtain information extracted from the content metadata, including the content ID, license ID, and policies.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "License Server URL in metadata: + "/flashaccess/license/v4". If protocol version 3 is the maximum supported by either the client or server, Adobe Access clients will send authentication requests to “License Server URL in metadata” + “/flashaccess/license/v3”. Otherwise, authentication requests are send to “License Server URL in metadata” + “/flashaccess/license/v1”

If an error occurs while parsing the request, a `HandlerParsingException` is thrown. This exception contains error information to be returned to the client. To retrieve the error information, call `HandlerParsingException.getErrorData()`. If an error occurs while generating a license because the policy requirements have not been satisfied, a `PolicyEvaluationException` is thrown. This exception also includes `ErrorData` to be returned to the client. See the API documentation for `LicenseRequestMessage.generateLicense()` for details on how policies are evaluated during license generation.

Licenses and errors are sent at one time when `LicenseHandler.close()` is called.

A device may have multiple licenses for the same content (same License ID), but can only have one license for a particular License ID and Policy ID. If it receives a license with a duplicate LicenseID/PolicyID, the new license will replace the old one only if the new license's issue date is later than the existing license's issue date. This logic is used to process licenses embedded into content, therefore, it is not recommended to embed more than one license with the same Policy ID in a chunk of content. The same logic applies to licenses passed to the client through the `DRMManager.storeVoucher()` ActionScript3 API; if the client already possesses a license with a later issue date, the provided license may be ignored.
