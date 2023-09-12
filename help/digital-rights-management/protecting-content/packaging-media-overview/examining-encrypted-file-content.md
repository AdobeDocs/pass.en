---
title: Examining encrypted file content
description: Examining encrypted file content
copied-description: yes
exl-id: df1fd04d-016e-4770-bcb9-97bfe2d39260
---
# Examining encrypted file content{#examining-encrypted-file-content}

You can examine the contents of an encrypted media file using using the Java API.

To examine encrypted file content:

1. Set up your development environment and include all of the JAR files. See *Setting up the SDK* for your project. 
1. Create a `MediaEncrypter` instance. 
1. Pass the encrypted file to the `MediaEncrypter.examineEncryptedContent` method, which returns a `KeyMetaData` object. 

1. Inspect the information within the `KeyMetaData` object.

For sample code that describes how to extract DRM metadata from an encrypted file, see `com.adobe.flashaccess.samples.mediapackager.ExamineContent` in the Reference Implementation Command Line Tools [!DNL samples/] directory.
