---
title: Encrypting content
description: Encrypting content
copied-description: yes
exl-id: 84a490ae-af0c-43c5-a849-ed832e83a28d
---
# Encrypting content{#encrypting-content}

Encrypting FLV and F4V content involves the use of a `MediaEncrypter` object. You can also package FLV and F4V files that contain only audio tracks. When encrypting H.264 content for lower-end devices, it may be practical to apply only partial encryption to improve performance. In such cases, an F4V file may be partially encrypted using the `F4VDRMParameters.setVideoEncryptionLevel`method.

To encrypt an FLV or an F4V file by using the Java API, perform the following steps:

1. Set up your development environment and include all of the JAR files mentioned in Setting up the development environment within your project. 
1. Create a `ServerCredential` instance to load the credentials needed for signing. 
1. Create a `MediaEncrypter` instance. Use a `MediaEncryperFactory` if you do not know what type of file you have. Otherwise you can create an `FLVEncrypter` or `F4VEncrypter` directly. 
1. Specify the encryption options by using a `DRMParameters` object. 
1. Set the signature options using a `SignatureParameters` object and pass the `ServerCredential` instance to its `setServerCredentials` method. 
1. Set the key and license information using an `V2KeyParameters` object. Set the policies using the `setPolicies` method. Set the information needed by the client to contact the license server by calling the `setLicenseServerUrl` and `setLicenseServerTransportCertificate` methods. Set the CEK encryption options using the `setKeyProtectionOptions` method, and its custom properties using the `setCustomProperties` method. Finally, depending on the type of encryption used, cast the `DRMKeyParameters` object to one of `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`, or `F4VDRMParameters`, and set the encryption options. 
1. Encrypt the content by passing the input and output files and encryption options to the `MediaEncrypter.encryptContent` method.

For sample code demonstrating how to encrypt content, see `com.adobe.flashaccess.samples.mediapackager.EncryptContent` in the Reference Implementation Command Line Tools “samples” directory.
