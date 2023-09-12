---
title: Issuing Domain-bound licenses
description: Issuing Domain-bound licenses
copied-description: yes
exl-id: b9823ae4-d88f-4580-a2ce-275ed3e32f51
---
# Issuing Domain-bound licenses{#issuing-domain-bound-licenses}

In order to issue a license using a policy that requires domain registration, the client's request must include a valid domain token issued by the domain server specified in the policy. When the client requests a license, it will automatically include its domain tokens for any domain server specified in the content metadata, if it has registered with those domain servers. If the selected policy requires domain registration, the SDK will automatically select a domain token from the request to bind the license to, or return an error if no appropriate domain token was found.

A domain token is considered to be valid if it is not expired and if it was issued by an authorized Domain CA. The license server must specify the domain authorities from which it will accept domain tokens by configuring `HandlerConfiguration.setDomainCAs()`. If no Domain CAs are configured, the license server will not be able to issue domain-bound licenses.

If the metadata includes multiple policies, the license server business logic could select a policy based on whether the client presented a domain token. Use `LicenseRequestMessage.getDomainTokens()` to determine the domains with which the client has registered.
