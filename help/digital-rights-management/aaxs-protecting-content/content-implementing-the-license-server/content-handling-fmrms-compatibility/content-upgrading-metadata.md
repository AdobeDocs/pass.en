---
title: Upgrading metadata
description: Upgrading metadata
copied-description: yes
exl-id: 04b3fb22-489e-41bb-95d0-99375f92fbae
---
# Upgrading metadata{#upgrading-metadata}

If an Adobe Access client encounters content packaged with Flash Media Rights Management Server 1.x, it will extract the encryption metadata from the content and send it to the server. The server will convert the FMRMS 1.x metadata into the Adobe Access format and send it back to the client. The client then sends the updated metadata in a standard Adobe Access license request.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`. 
* The request URL is "*Base URL from 1.x content*" +"/flashaccess/headerconversion/v1".

The metadata conversion could be done on the fly when the server receives the old metadata from the client. Alternatively, the server could preprocess the old content and store the converted metadata; in this case, when the client requests new metadata, the server just needs to fetch the new metadata matching the license identifier of the old metadata.

To convert metadata, the server must perform the following steps:

* Get `LiveCycleKeyMetaData`. To pre-convert the metadata, `LiveCycleKeyMetaData` can be obtained from a 1.x packaged file using `MediaEncrypter.examineEncryptedContent()`. The metadata is also included in the metadata conversion request ( `FMRMSv1MetadataHandler.getOriginalMetadata()`). 
* Get the license identifier from the old metadata, and find the encryption key and policies (this information was originally in the Adobe LiveCycle ES database. The LiveCycle ES policies must be converted to Adobe Access 2.0 policies.) The Reference Implementation includes scripts and sample code for converting the policies and exporting license information from LiveCycle ES. 
* Fill in the `V2KeyParameters` object (which you retrieve by calling `MediaEncrypter.getKeyParameters()`). 
* Load the `SigningCredential`, which is the packager credential issued by Adobe used to sign encryption metadata. Get the `SignatureParameters` object by calling `MediaEncrypter.getSignatureParameters()` and fill in the signing credential. 
* Call `MetaDataConverter.convertMetadata()` to obtain the `V2ContentMetaData`. 
* Call `V2ContentMetaData.getBytes()` and store for future use, or call `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
