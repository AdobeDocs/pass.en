---
title: Handling Domain Registration requests
description: Handling Domain Registration requests
copied-description: yes
exl-id: f846e154-e90c-4e45-aafd-f6e22dac3339
---
# Handling Domain Registration requests{#handling-domain-registration-requests}

If the DRM metadata indicates that domain registration is needed to play the content, the client application should invoke the DRMManager.addToDeviceGroup() ActionScript API or joinLicenseDomain() iOS API. If the client has not yet registered with the specified domain server (or if the application is forcing a re-join), a domain registration request is sent. The domain server determines whether the client is permitted to join a domain and issues one or more domain credentials to the client.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "Domain Server URL in metadata: + "/flashaccess/domain/v4". Otherwise, the request URL is Domain Server URL in metadata” + “/flashaccess/domain/v3”

When initializing the `DomainRegistrationHandler`, the domain server URL must be specified. This URL will be included in the domain tokens issued by the handler to indicate the domain server that issued the token. The URL must match the domain server URL specified in any policy that requires domain registration with the server.

To determine whether the client is permitted to join the domain, the server may examine the machine and user information in the request. See [Using machine identifiers](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) for information on how to identify and count machines joining the domain. The server may also determine which domain the client is permitted to join. Note that a client may only be a member of one domain per domain server URL. If the machine already has a domain token for this domain server URL, the domain registration request will include the current domain name ( `getRequestDomainName()`). For a re-join request, the domain server must either return the current set of domain credentials for this domain or return an error (the domain server may not return the domain credentials for a different domain).

If the domain server requires authentication to join a domain, the request should contain an authentication token. Just as with a license request, domain registration may require username/password or custom authentication. See [User authentication](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) for details on handling authentication tokens.

The domain server is responsible for storing and managing the domain keys associated with each domain. When a new key pair needs to be generated for a domain (the first domain registration for the domain), invoke `generateDomainCredential` `(String, int, Principal, Date)`. This method will generate a new domain key pair and domain certificate. The domain server must store the private key and certificate and provide those objects when processing subsequent requests for this domain. It is also possible to generate a new key pair for a domain in order to roll over the keys. When rolling over the keys for a particular domain, be sure to increment the key version in `generateDomainCredential` as well.

Each subsequent time a machine registers with the same domain, the same domain private key and certificate should be used. Invoke `addDomainCredential(DomainToken, PrivateKey)` to return an existing domain credential to the client. If there are multiple domain credentials for the domain because the domain keys were changed, the server should provide domain credentials for the current domain key and all previous domain keys so the client can consume licenses bound to older domain keys. This enables a license bound to an old domain token to be moved to a newly registered machine and still be playable.
