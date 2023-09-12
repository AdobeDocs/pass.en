---
description: Information about packaging and protection of content allows you to protect your content.
title: Packaging and protecting comtent
exl-id: f33d382b-07d7-4630-9e44-820d6249fee4
---
# Packaging and protecting content {#packaging-protecting-content}

Information about packaging and protection of content allows you to protect your content.

## Securing the server {#securing-the-server}

You need to physically secure the computer on which policy management and content packaging occurs.

For more information, see [Physical security and access](../../secure-deployment-guidelines/physical-sec-and-access.md).

If your content packaging implementation requires network connectivity, you must harden your operating system and implement an appropriate firewall solution. For more information, see [Network topology](../../secure-deployment-guidelines/overview/network-topology.md).

## Securely packaging content {#securely-packaging-content}

The configuration file for the Adobe Primetime DRM Media Packager command-line tool requires a PKCS12 credential that is used during packaging.

In the Reference Implementation command-tine tools, the password for the PKCS12 credentials file is stored in the `flashaccess.properties` file in clear text. For this reason, take extra care when you secure the computer that hosts this file and ensure that the computer is in a secure environment. For more information, see [Physical security and access](../../secure-deployment-guidelines/physical-sec-and-access.md).

The packager also uses the License Server and License Server Transport certificates, and the integrity and confidentiality of this information must be protected. Only authorized entities should be permitted to use the packager. If your private keys are compromised, inform Adobe Systems Incorporated immediately so that the certificate can be revoked.

>[!NOTE]
>
>The API enables you to use the same key for multiple pieces of content. To ensure the highest level of security, you should only use this feature for multi-bit rate FMS content. Do not use the same key for multiple files that represent different content.

The Primetime DRM Packaging API issues warnings under certain conditions. Review these warnings to determine whether your files have been successfully encrypted. The warning messages might be one of the following:

* The policy has expired and an unrecognized tag or track cannot be encrypted.
* Movie fragments cannot be encrypted and references inside those fragments might beinvalid.
* Metadata cannot be encrypted.

If content is packaged by using a policy with incorrect attributes, the policy needs to be updated. The updated policy must be made available to the License Server though a policy update list or another delivery mechanism. Some policy attributes cannot be changed after the policy is created. If these attributes are incorrect, pull the content back from the distribution sites, revoke the policy so that no future licenses can be granted, and encrypt the content again.

When packaging is complete, the packaging key is garbage-collected, and is not explicitly destroyed. As a result, the packaging key remains present in memory for some time. You must guard against unauthorized access to the machine and ensure that you do not expose any files, such as core dumps, that might reveal this information.

## Securely storing policies {#securely-storing-policies}

The Adobe Primetime DRM SDK allows you to develop applications that can be used in content packaging and policy creation.

When you create these applications, you can allow some users to create and modify policies, and limit other users to only applying existing policies to the content. You must implement the necessary access controls and create user accounts with different privileges for policy creation and policy application.

Policies are not signed or protected from modification until they are used in packaging. If you are concerned that packaging tool users might modify policies, sign the policies to ensure that the policies cannot be modified.

For more information about creating applications with the SDK, see the Primetime DRM APIs on [API Primetime API References](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Asymmetric key encryption {#asymmetric-key-encryption}

Asymmetric key encryption, also called public key encryption, uses pairs of keys. One key is for encryption, and the other key is for decryption.

The decryption key, or the *`private key`*, is kept secret; the encryption key, or the *`public key`*, is made available to anyone who is authorized to encrypt content. Anyone with access to the public key can encrypt content. However, only someone with access to the private key can decrypt the content. The private key cannot be reconstructed from the public key.

When you package content, the License Server's public key is used to encrypt the content encryption key (CEK) in the DRM metadata. You must ensure that only the License Server has access to the License Server's private key. If someone else has the key, they can decrypt and view the content.

>[!CAUTION]
>
>Make sure that you obtain the License Server's certificate that includes the public key from a trusted source. This way, you can ensure that it is the License Server's key and not a rogue public key. If attackers were to substitute their public key for the License Server's key, they could decrypt your content.

For more information about how to package content, see [Using the Adobe Primetime DRM SDK for Protecting Content](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
