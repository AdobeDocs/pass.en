---
description: Setting policies is the process of specifying conditions for when and how a user is allowed to play protected video content.
title: Setting policies
exl-id: ab7295c8-88f2-4d4a-a7f1-3332df7bb735
---
# Setting policies{#setting-policies}

Setting policies is the process of specifying conditions for when and how a user is allowed to play protected video content.

Policy creation occurs as part of your license token request. (See [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) for an example using Widevine).

Once a customer's server-side code has determined that it will issue a license (based on entitlements checks, geolocation, or any other required information), then it requests a token, and *in the token* it specifies the required `securityLevel`, `hdcpOutputControl`, and `licenseDuration`. Those are the client-side options for a Widevine policy. Other DRM solutions offer similar approaches, but the details are different in each case, and are elaborated upon in the individual workflows.

>[!NOTE]
>
>Adobe provides a sample reference server that shows how to implement your own entitlement server / storefront: [Reference Server: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
