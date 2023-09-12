---
title: Enhanced License Chaining
description: Enhanced License Chaining
copied-description: yes
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
---
# Enhanced License Chaining {#enhanced-license-chaining}

If a DRM policy is used to generate a license that supports license chaining, the server must decide whether to issue a Leaf license, Root license, or both. If you want to determine what type of license chaining a DRM policy supports, you must use `Policy.getLicenseChainType()`, or call `Policy.getRootLicenseId()` to determine if the DRM policy has a root license. With Adobe Primetime DRM 2.0 license chaining, the server typically issues a leaf license the first time that a user requests a license for a particular machine and a root license thereafter. If you want to determine if the machine already has a leaf license for the specified policy, you need to call `LicenseRequestMessage.clientHasLeafForPolicy()`.

With enhanced license chaining in Adobe Primetime DRM 3.0, it is recommended to issue both a Leaf and a Root the first time the user requests a license for a particular machine. If the user already has the Root license, the server may issue only a Leaf (call `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` to determine if the client already has a 3.0 Enhanced Root). For subsequent license requests, the client then indicates that it already has a Leaf and a Root, so the server should issue a new Root license. When the enhanced license chaining is used, `setRootKeyRetrievalInfo()` must be called to provide the credentials needed to decrypt the root encryption key in the DRM policy.

>[!NOTE]
>
>If the policy supports 3.0 Enhanced License Chaining, but the client is Primetime DRM 2.0, the server then issues a 2.0 original chained license. To determine the client version, use `LicenseRequestMessage.getClientVersion()`.
