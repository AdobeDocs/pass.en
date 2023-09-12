---
description: There are two types of requests related to Flash Media Rights Management Server 1.x compatibility. One type of request is used to prompt 1.x clients to upgrade to a runtime that supports Adobe Primetime DRM 2.0 or later. Another is used to update 1.x metadata to the Primetime DRM format before a license can be requested. Support for these requests is only needed if you previously deployed any content that uses FMRMS 1.0 or 1.5.
title: Handling FMRMS compatibility
---

# Handling FMRMS compatibility {#handling-fmrms-compatibility}

There are two types of requests related to Flash Media Rights Management Server 1.x compatibility. One type of request is used to prompt 1.x clients to upgrade to a runtime that supports Adobe Primetime DRM 2.0 or later. Another is used to update 1.x metadata to the Primetime DRM format before a license can be requested. Support for these requests is only needed if you previously deployed any content that uses FMRMS 1.0 or 1.5.

## Upgrading clients {#upgrading-clients}

If an FMRMS 1.x client contacts a Adobe Primetime DRM server, the server needs to prompt the client to upgrade.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`. 
* The request URL is "*Base URL from 1.x content*" + " [!DNL /edcws/services/urn:EDCLicenseService]"

  Unlike other Adobe Primetime request handlers, this handler does not provide access to any request information or require any response data to be set. Create an instance of the `FMRMSv1RequestHandler`, and then call `close()`

## Upgrading metadata {#upgrading-metadata}

If an Adobe Primetime DRM client encounters content packaged with Flash Media Rights Management Server 1.x, it then extracts the encryption metadata from the content and sends it to the server. The server then converts the FMRMS 1.x metadata into the Primetime DRM format and sends it to the client. The client then sends the updated metadata in a standard Primetime DRM license request.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`. 
* The request URL is "*Base URL from 1.x content*" +" [!DNL /flashaccess/headerconversion/v1]".

The metadata conversion could be done on the fly when the server receives the old metadata from the client. Alternatively, the server could preprocess the old content and store the converted metadata; in this case, when the client requests new metadata, the server just needs to fetch the new metadata matching the license identifier of the old metadata.

To convert metadata, the server must perform the following steps:

* Get `LiveCycleKeyMetaData`. To pre-convert the metadata, `LiveCycleKeyMetaData` can be obtained from a 1.x packaged file using `MediaEncrypter.examineEncryptedContent()`. The metadata is also included in the metadata conversion request ( `FMRMSv1MetadataHandler.getOriginalMetadata()`). 

* Get the license identifier from the old metadata, and find the encryption key and DRM policies (this information was originally in the Adobe LiveCycle ES database. The LiveCycle ES DRM policies must be converted to Primetime DRM 2.0 DRM policies.) The Reference Implementation includes scripts and sample code for converting the DRM policies and exporting license information from LiveCycle ES. 
* Fill in the `V2KeyParameters` object (which you retrieve by calling `MediaEncrypter.getKeyParameters()`). 

* Load the `SigningCredential`, which is the packager credential issued by Adobe used to sign encryption metadata. Get the `SignatureParameters` object by calling `MediaEncrypter.getSignatureParameters()` and fill in the signing credential. 

* Call `MetaDataConverter.convertMetadata()` to obtain the `V2ContentMetaData`. 

* Call `V2ContentMetaData.getBytes()` and store for future use, or call `FMRMSv1MetadataHandler.setUpdatedMetadata()`.