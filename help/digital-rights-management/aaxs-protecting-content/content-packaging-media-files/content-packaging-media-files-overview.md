---
title: Overview
description: Overview
copied-description: yes
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
---
# Overview {#overview}

*Packaging* refers to the process of encrypting and applying a policy to FLV or F4V files. Use the media packaging APIs to package files. The Adobe Access Java SDK can only package progressive-download Flash and AIR content, such as FLV, F4V, and MP4. In order to package content using Adobe Access DRM for other content formats, such as Adobe HTTP Dynamic Streaming (HDS) or Apple HTTP Live Streaming (HLS), you will have to use other tools, such as Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) or an encoder that implements the Adobe Broadcast SDK ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Alternatively, customers have the choice of using Adobe's Java Primetime Packager toolset, which can package content for a variety of target formats, such as HDS, HLS, and DASH.

Packaging is de-coupled from the license server. There is no need for the packager to connect to the license server to exchange any information about the content. Everything the license server needs to know to issue the license is included in the content metadata.

When a file is encrypted, its contents cannot be parsed without the appropriate license. Adobe Access allows you to select which parts of the file to encrypt. Because Adobe® Access™ can parse the file format of the FLV and F4V content, it can intelligently encrypt selective parts of the file instead of the entire file as a whole. Data such as metadata and cue points can remain unencrypted so that search engines can still search the file.

It is possible for a given piece of content to have multiple policies. This could be useful, for example, if you would like to license content under different business models without having to package the content multiple times. For example, you could allow anonymous access for a short period of time, and after that allow the customer to buy the content and have unlimited access. If content is packaged using multiple policies, the License Server must implement logic for selecting which policy to use to issue a license.

>[!NOTE]
>
>The architecture allows for usage policies to be specified and bound to content when the content is packaged. Before a client can play back content, the client must acquire a license for that computer. The license specifies the usage rules that are enforced and provides the key used to decrypt the content. The policy is a template for generating the license, but the license server may choose to override the usage rules when issuing the license. Note that the license may be rendered invalid by such constraints as expiration times or playback windows.

There are numerous options available when packaging content. These are specified in the `DRMParameters` interface and the classes implementing that interface, which are the `F4VDRMParameters` and `FLVDRMParameters`. With these classes you can set signature and key parameters, as well as indicate whether to encrypt audio content, video content, or script data. To see how these are implemented in the reference implementation, see the descriptions of the Media Packager command line options discussed in *Using the Adobe Access Reference Implementations*. These options are based on the Java API and are therefore available for programmatic usage.

The packaging options include:

* Encryption options (audio, video, partial encryption). 
* License server URL (the client uses this as the base URL for all requests sent to the license server) 
* License server transport certificate 
* License sever certificate, used to encrypt the CEK. 
* Packager credential for signing metadata

Adobe Access provides an API for passing in the CEK. If no CEK is specified, the SDK randomly generates it. Typically you need a different CEK for each piece of content. However, in Dynamic Streaming, you would likely use the same CEK for all the files for that content, so the user only needs a single license and can seamlessly transition from one bit rate to another. To use the same key and license for multiple pieces of content, pass the same `DRMParameters` object to `MediaEncrypter.encryptContent()`, or pass in the CEK using `V2KeyParameters.setContentEncryptionKey()`. To use a different key and license for each piece of content, create a new `DRMParameters` instance for each file.

When packaging content using key rotation, you can control the Rotation Keys used and how often the keys change. `F4VDRMParameters` and `FLVDRMParameters` implement the `KeyRotationParameters` interface. Through this interface, you can enable key rotation. You also need to specify a `RotatingContentEncryptionKeyProvider`. For each sample encrypted, this class determines the Rotation Key to use. You may implement your own provider, or use the `TimeBasedKeyProvider` included with the SDK. This implementation randomly generates a new key after a specified number of seconds.

In some cases you may need to store the content metadata as a separate file and make it available to the client separate from the content. To do this, invoke `MediaEncrypter.encryptContent()`, which returns a `MediaEncrypterResult` object. Call `MediaEncrypterResult.getKeyInfo()` and cast the result to `V2KeyStatus`. Then retrieve the content metadata and store it in a file.

All of these tasks can be accomplished using the Java API. For details about the Java API discussed in this chapter, see *Adobe Access API Reference*.

For information about the Media Packager reference implementation, see *Using the Adobe Access Reference Implementations*.
