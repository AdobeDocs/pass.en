---
title: Issuing domain-bound licenses
description: Issuing domain-bound licenses
copied-description: yes
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
---
# Issuing domain-bound licenses{#issuing-domain-bound-licenses}

To issue a license using a DRM policy that requires domain registration, the client's request must include a valid domain token issued by the domain server specified in the policy. When the client requests a license, it automatically includes its domain tokens for any domain server that is specified in the content metadata provided it has registered with those domain servers. If the selected DRM policy requires domain registration, the SDK then automatically selects a domain token from the request to bind the license to or returns an error if no appropriate domain token has been found.

A domain token is considered to be valid if it is not expired and if it was issued by an authorized Domain CA. The license server must specify the domain authorities from which it then accepts domain tokens by configuring `HandlerConfiguration.setDomainCAs()`. If no Domain CAs are configured, the license server will not be able to issue domain-bound licenses.

If the metadata includes multiple DRM policies, the license server business logic could select a DRM policy that is based on whether the client presented a domain token. You can use `LicenseRequestMessage.getDomainTokens()` to determine the domains with which the client has registered.
