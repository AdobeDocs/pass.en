---
title: Packaging media files overview
description: Packaging media files overview
copied-description: yes
exl-id: 88c593a7-33b5-4773-b283-2ab16f9e8c3a
---
# Overview {#packaging-media-files-overview}

 Packaging refers to the process of encrypting and applying a DRM policy to video content. You can use the media packaging APIs to package files. The Primetime DRM Java SDK can only package progressive-download content, such as MP4.

>[!NOTE]
>
>Be sure to contact your Primetime DRM representative on how to select the most appropriate packaging option for your media format and use cases.

Packaging is de-coupled from the license server. There is no need for the packager to connect to the license server to exchange any information about the content. Everything the license server needs to know to issue a license is included in the content metadata.

When a file is encrypted, its contents cannot be parsed without the appropriate license. You can use Primetime DRM to select the parts of the file that you want to encrypt. Because Primetime DRM can parse the file format of the video content, it can intelligently encrypt selective parts of a file instead of an entire file. Data, such as metadata and cue points, can remain unencrypted so that search engines can still search the file.

A specified piece of content may have multiple DRM policies. For example, you can license content under different business models without having to package the content multiple times. Additionally, you could allow anonymous access for a short period of time and then allow the customer to buy the content to have unlimited access. If content is packaged by using multiple DRM policies, the License Server must implement logic for selecting which DRM policy must be used to issue a license.

>[!NOTE]
>
>The architecture allows for usage DRM policies to be specified and bound to content when the content is packaged. Before a client can play back content, the client must acquire a license for a specified computer. The license specifies the usage rules that are enforced and provides the key that must be used to decrypt content. The DRM policy represents a template for generating a license. However, the license server may override the usage rules when it issues a license. The license may be rendered invalid by such constraints, such as expiration times or playback windows.

Primetime DRM provides an API for passing in the CEK. If no CEK is specified, the SDK randomly generates it. Typically you need a different CEK for each section of content. However, in Dynamic Streaming, you are likely to use the same CEK for all the files that make up that content. Therefore a user only needs a single license to transition seamlessly from one bit rate to another. If you want to use the same key and license for multiple pieces of content, you need to pass the same `DRMParameters` object to `MediaEncrypter.encryptContent()`, or pass in the CEK using `V2KeyParameters.setContentEncryptionKey()`. If you want to use a different key and license for each section of content, you need to create a new `DRMParameters` instance for each file.

When you package content using key rotation, you can control the Rotation Keys that are used and the frequency with which the keys change. `F4VDRMParameters` and `FLVDRMParameters` implement the `KeyRotationParameters` interface. Through this interface, you can enable key rotation. You also need to specify a `RotatingContentEncryptionKeyProvider`. For each sample encrypted, this class determines the Rotation Key to use. You may implement your own provider, or use the `TimeBasedKeyProvider` included with the SDK. This implementation randomly generates a new key after a specified number of seconds.

In some cases you may need to store the content metadata as a separate file and make it available to the client separate from the content. In that case, you need to invoke `MediaEncrypter.encryptContent()`, which returns a `MediaEncrypterResult` object. Call `MediaEncrypterResult.getKeyInfo()` and cast the result to `V2KeyStatus`. Then retrieve the content metadata and store it in a file.

All of these tasks can be accomplished with the Java API.

See *Adobe Primetime DRM API Reference* for details about the Java API.

See *Using the Adobe Primetime DRM Reference Implementations* for information about the Media Packager reference implementation.
