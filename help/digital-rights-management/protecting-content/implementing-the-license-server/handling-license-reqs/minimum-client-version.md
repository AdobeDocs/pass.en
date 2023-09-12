---
title: Minimum client version
description: Minimum client version
copied-description: yes
exl-id: c4aebafe-33b4-4da3-9e79-53d6a7e9f22d
---
# Minimum client version {#minimum-client-version}

Adobe Primetime DRM 2.0.2 and higher introduce some new usage rules, which are not understood by Primetime DRM 2.0 clients. By setting the minimum supported client version ( `HandlerConfiguration.setMinSupportedClientVersion()`), the license server can control how older clients behave when they encounter licenses with these usage rules. Based on this setting, the server can indicate whether older clients can ignore the usage rules they do not understand or whether older clients will not be able to consume licenses with those usage rules.

For example,

* If the license specifies the device capabilities requirements ( [Device capabilities required to play protected content](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), Primetime DRM clients 2.0.2 and higher can enforce those requirements. 
* If the license server does not want content to play on clients that do not understand the device capabilities requirements , set the minimum supported client version to 2 (for 2.0.2). This will prevent the server from issuing licenses to Primetime DRM clients before 2.0.2. The minimum client version is also enforced if the license is transferred from one client to another. 
* If the license server wants to allow older clients to ignore the device capabilities requirements, set the minimum supported client version to 1 (for Primetime DRM 2.0). The server then issues a license to any client version 2.0 and higher. If the client upgrades or transfers the license to another client with version 2.0.2 or later, the device capabilities requirements in the license is then enforced because the client can then support that usage rule.
