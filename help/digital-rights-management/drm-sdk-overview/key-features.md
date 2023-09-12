---
title: Key features
description: Key features
copied-description: yes
exl-id: 3d9af53c-97ab-425d-9a01-128e0f112ec1
---
# Key features{#key-features}

Adobe Primetime DRM provides these key features:

* **HLS Streaming Support (requires Adobe Primetime):** Use Primetime DRM with HLS content that can be streamed to any platform supported by Flash or Adobe Primetime (such as Desktop, iOS, and Android). 
* **Native iOS Application Support (requires Adobe Primetime):** Use Primetime DRM to protect video in your iOS applications. 
* **Native Android Application Support (requires Adobe Primetime):** Use Primetime DRM to protect video in your Android applications. 
* **Protected Streaming on Xbox (requires Adobe Primetime)**. 
* **Remote iOS key delivery (requires Adobe Primetime):** Support for delivering remote iOS keys through a multi-tenant key server, called the Primetime DRM Key Server. 
* **Persistent content protection:** Content remains protected throughout the distribution chain. Once the content is packaged, it remains protected at all times, and portions of it are only decrypted at the time of playback and in accordance with the usage rules. 
* Because the content is packaged with usage rules and licensing information, protection always travels with the content. If unlicensed consumers attempt to play the content, the policy embedded in the content redirects them so they can acquire a valid license for the content. 
* **Secure playback of protected content:** Proven encryption schemes are used to protect content from unauthorized playback. 
* **Flexible usage rules:** Usage rules determine how consumers can use protected content. The usage rules supported by Primetime DRM allow for several different business models, including pay-per-view, movie rental, subscriptions, or ad-funded services. The usage rules are specified by the policy you embed into the content during packaging, or can be specified by the License Server during license acquisition. 
* **Output protection:** Output protection controls can be used to engage protection schemes such as HDCP, CGMS-A or Rovi (formerly Macrovision) ACP. This can help protect content output over digital (for example, HDMI, DVI, and UDI) and analog (for example, S-Video, and Component Video) outputs.

  You can specify output protection options in the policy you create for your content, allowing or disallowing access to content based on a device's output protection capabilities. For example, you can specify that output protection is not required for certain content, but require output protection for premium video content, preventing the output of content on operating systems that lack this capability.

  While these rules are consistently enforced across all platforms, currently it is only possible to securely turn on output protection on Windows platforms. 

* **Support for dynamic streaming:** Use the dynamic streaming feature of Flash Media Server or Adobe HTTP Dynamic Streaming to protect content encoded at multiple bit rates. Dynamic streaming uses a video stream that dynamically adjusts the bit rate and playback quality based on available bandwidth, providing an improved user experience. Primetime DRM makes it possible use the same Content Encryption Key and license across the different encodings of the same asset. 
* **Offline viewing:** The Adobe AIR runtime client allows consumers to download and store content for later viewing, whether or not the computer remains connected to the Internet. 
* **Identity-based licensing:** Links permissions to user identities, requiring consumers to authenticate themselves (providing a user id and password) in order to gain access to content. Identity-based licensing requires that the party developing the client application implement user authentication as part of the license acquisition workflow. 
* **License chaining:** Allows consumers to extend the life of all of their content by renewing a single root license. One of the primary uses of license chaining is for subscription-based business models, where, at the end of a subscription period, licenses to large numbers of content files can be renewed by simply renewing the root license.

  Both root and leaf licenses are bound to the consumer's computer. The leaf license contains the CEK and a reference to the root license. The root license can extend the rights granted in the leaf license. For example, a consumer may have leaf licenses for 50 pieces of content that will expire at the end of a given subscription period. If the consumer downloads a new root license with a new expiration date, all 50 pieces of content can be played back until the updated license expires.

  Primetime DRM 2.0 introduced license chaining in which both the leaf and root licenses are bound to a specific machine. Primetime DRM 3.0 introduces an enhanced form of license chaining, in which a leaf is bound to a root license, and only the root license is bound to a specific machine or domain. Read *Enhanced License Chaining* in *Using the Adobe Primetime DRM SDK for Protecting Content*. 

* **Key rotation:** During typical packaging, the content is encrypted using the Content Encryption Key (CEK), and the client obtains a license containing the CEK in order to consume the content. When key rotation is enabled, the key used to encrypt the content can be changed so that the key is only used to encrypt a portion of the content. Read *Key Rotation* in *Using the Adobe Primetime DRM SDK for Protecting Content*. 

* **Out-of-band Licenses:** With Primetime DRM, it is possible to implement a workflow in which clients obtain pre-generated licenses out-of-band, eliminating the need to deploy a License Server. 
* **Domain Support:** As an alternative to binding a license to a specific device, Primetime DRM supports binding licenses to a domain. Multiple devices may join a domain and receive a domain token allowing licenses to be moved between devices in the domain. Read *Domain Registration* in *Using the Adobe Primetime DRM SDK for Protecting Content*. 

* **Partial encryption:** Specifies whether all frames, or only a subset of frames, should be encrypted. There are three levels of encryption: low, medium and high. Reducing the encryption level may decrease CPU overhead on lower end machines. 
* **Disconnected content packaging:** Content packaging does not require a network connection to the License Server. This enables secure back-end operations by limiting the exposure of compressed content that has not yet been protected. 
* **Control over clock rollback: **Primetime DRM provides for the secure and accurate calculation of time to detect clock rollback on the client computer. This enforces rights related to accessing content for a specific amount of time, and prevents consumers from subverting access rights by altering the time on their computer. 
* **Individualization**: Allows binding content to a particular machine. 
* **Application allow list:** Allows the client runtime to ensure that protected content only plays within an authorized SWF or AIR application. 
* **Revocation of compromised clients:** Compromised client software can be revoked. If the Flash Player or Adobe AIR runtime is determined to have been compromised, service can be refused to those clients until they upgrade to a newer and more secure version of the client software. 
* **Multiple policies for the same video file:** A single piece of video content can have multiple policies embedded during packaging. When issuing a license, the License Server may decide which of the policies to use, enabling a content distributor to use the same protected file for different business models (such as rental and electronic sell-through).
