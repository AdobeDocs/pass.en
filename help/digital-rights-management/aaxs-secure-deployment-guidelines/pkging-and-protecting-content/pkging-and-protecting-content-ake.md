---
title: Asymmetric key encryption
description: Asymmetric key encryption
copied-description: yes
exl-id: 5962176e-07ec-4606-b1d8-39946ba59127
---
# Asymmetric key encryption{#asymmetric-key-encryption}

Asymmetric key encryption (also called public key encryption) uses pairs of keys. One key is used for encryption; the other for decryption. The decryption key is kept secret, and is referred to as a *private key*. The encryption key, referred to as the *public key*, is made available to anyone authorized to encrypt content. Anyone with access to the public key is able to encrypt content, but only someone with access to the private key can decrypt the content. The private key cannot be reconstructed from the public key.

When packaging content, the License Server's public key is used to encrypt the content encryption key (CEK) in the DRM metadata. You must ensure that only the License Server has access to the License Server's private key; if someone else has the key they can decrypt and view the content.

***Caution:** Ensure that you obtain the License Server's certificate (containing the public key) from a trusted source so that you can be certain it is the License Server's key, and not a rogue public key. If an attacker were to substitute their public key for the License Server's key, they would be able to decrypt your content.*

For more information on packaging content, see *Using the Adobe Access SDK for Protecting Content*.
