---
description: The following encryption options are selected at packaging time and cannot be modified during license acquisition.
title: Key Rotation
exl-id: bcb90f0e-5c61-4c56-a030-2831d9a2a962
---
# Key Rotation{#key-rotation}

The following encryption options are selected at packaging time and cannot be modified during license acquisition.

During packaging, typically the content is encrypted using the Content Encryption Key (CEK), and the client obtains a license containing the CEK in order to consume the content. When key rotation is enabled, the Rotation Key is used to encrypt the content, and the key can be changed so that each Rotation Key is only used to encrypt a portion of the content. The Rotation Keys are protected using the Content Encryption Key, and the client still obtains a single license containing the CEK in order to consume the content. The packager implementation can control the Content Encryption Key and Rotation Keys used, as well as the frequency with which the Rotation Keys change.

Content packaged using key rotation can only be played on Adobe Access clients version 3.0 and higher. Older clients would need to upgrade in order to play this content.
