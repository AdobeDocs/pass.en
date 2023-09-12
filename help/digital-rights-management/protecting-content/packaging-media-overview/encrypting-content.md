---
title: Encrypting content
description: Encrypting content
copied-description: yes
exl-id: c6b5d8c7-eda4-40c0-a609-0ebfeba90c04
---
# Encrypting content{#encrypting-content}

You encrypt video content with the `MediaEncrypter` object. You can encrypt media files that include only audio tracks. You can also apply only partial encryption; for example, to improve performance when you encrypt H.264 content for lower-end devices.

To encrypt media files using the Java API:

1. Set up your development environment and include all of the JAR files mentioned in *Setting up the development environment* within your project. 
1. Create a `ServerCredential` instance to load the credentials needed for signing. 
1. Create a `MediaEncrypter` instance. Use a `MediaEncryperFactory` if you do not know what type of file you have. 

1. Specify the encryption options by using a `DRMParameters` object. 
1. Set the signature options using a `SignatureParameters` object and pass the `ServerCredential` instance to its `setServerCredentials` method. 

1. Set the key and license information using an `V2KeyParameters` object. Set the DRM policies using the `setPolicies` method. Set the information needed by the client to contact the license server by calling the `setLicenseServerUrl` and `setLicenseServerTransportCertificate` methods. Set the CEK encryption options using the `setKeyProtectionOptions` method, and its custom properties using the `setCustomProperties` method. Finally, depending on the type of encryption used, cast the `DRMKeyParameters` object to the appropriate type ( `VideoDRMParameters`, `AudioDRMParameters`), and set the encryption options. 

1. Encrypt the content by passing the input and output files and encryption options to the `MediaEncrypter.encryptContent` method.

For sample code that shows how to encrypt content, see `com.adobe.flashaccess.samples.mediapackager.EncryptContent` in the Reference Implementation Command Line Tools [!DNL samples/] directory.
