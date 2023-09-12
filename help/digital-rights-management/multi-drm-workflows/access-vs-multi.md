---
description: For those familiar with Adobe's Primetime Access DRM solution, there are some fundamental architectural differences between Access and the Primetime Cloud DRM, powered by ExpressPlay solution.
title: Migrating from Access to Multi-DRM
exl-id: f5e4cd88-091d-4049-933d-1c72ceeb2efb
---
# Migrating from Access to Multi-DRM {#migrating-from-access-to-multi-drm}

For those familiar with Adobe's Primetime Access DRM solution, there are some fundamental architectural differences between Access and the Primetime Cloud DRM, powered by ExpressPlay solution.

## Architectural Differences Between Access and Multi-DRM

|  | Access | Multi-DRM |
|---|---|---|
| **Packaging** | The Packager is bound to a license server. The Packager must know the public key of the license server when content is packaged. | The Packager is not bound to one license server. |
|  | Once content is packaged, it is bound to a particular license server. | Content is not bound to a specific license server. One effect of this is that you can package all of your content before obtaining your production license.  |
|  | The Packager does not need to communicate with any form of key storage, because the keys are securely embedded into the content itself (in metadata) after being encrypted. Only the corresponding license server can read them.  |Keys must be sent *to* Packagers from a key storage system, or sent *from* a Packager to a key storage system. A key storage system can be either a customer's own system, or it can be ExpressPlay's Key Storage. |
| **Entitlement** | The client makes a request for content to the Access Cloud service. The Access cloud service then makes a request to the customer's entitlement system. The customer's entitlement system responds back with entitlements for the customer. (The client has probably gotten a cookie for login from the customer's servers prior to making the license request.) |The client makes a request for a token from the customer's storefront (this is probably the same workflow in which the customer was previously getting an authentication cookie). At this time, the customer performs an entitlements check. If the entitlements check passes, the customer sends a request to the ExpressPlay servers to generate a token for the customer. This token is always bound to a specific piece of content, and *may* be bound to a specific device. The customer's storefront sends the token back to the client. When the client makes a DRM play request, the token is included in the request (the method for this is device-specific), and ExpressPlay's DRM server validates the token without calling out to the customer's server. |
