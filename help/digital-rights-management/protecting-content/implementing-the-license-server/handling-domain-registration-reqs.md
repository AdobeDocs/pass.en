---
title: Handle Domain Registration requests
description: Handle Domain Registration requests
copied-description: yes
exl-id: 6f4ed908-32ee-4c8b-8965-53381b737989
---
# Handle Domain Registration requests {#handle-domain-registration-requests}

If the DRM metadata indicates that domain registration is needed to play the content, the client application should invoke the `DRMManager.addToDeviceGroup()` ActionScript API or `joinLicenseDomain()` iOS API. If the client has not yet registered with the specified domain server (or if the application is forcing a re-join), a domain registration request is sent. The domain server determines whether the client is permitted to join a domain and issues one or more domain credentials to the client.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "Domain Server URL in metadata: + " [!DNL /flashaccess/domain/v4]". Otherwise, the request URL is Domain Server URL in metadata” + " [!DNL /flashaccess/domain/v3]"

When you initializie the `DomainRegistrationHandler`, you must specify the domain server URL. This URL is then included in the domain tokens issued by the handler to indicate to the domain server that the token has been issued. The URL must match the domain server URL specified in any DRM policy that requires domain registration with the server.

To determine whether the client is permitted to join the domain, the server may examine the machine and user information in the request. The server may also determine which domain the client is permitted to join.

>[!NOTE]
>
>A client may only be a member of one domain per domain server URL. If the machine already has a domain token for this domain server URL, the domain registration request includes the current domain name ( `getRequestDomainName()`).

For a re-join request, the domain server must either return the current set of domain credentials for this domain or return an error. The domain server may not return the domain credentials for a different domain.

See [Using machine identifiers](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) for information on how to identify and count machines joining the domain.

If the domain server requires authentication to join a domain, the request should contain an authentication token. Just as with a license request, domain registration may require username/password or custom authentication.

See [User authentication](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) for details on how to manage authentication tokens.

The domain server is responsible for storing and managing the domain keys that are associated with each domain. When a new key pair needs to be generated for a domain (the first domain registration for the domain), you need to invoke `generateDomainCredential(String, int, Principal, Date)`. This method generates a new domain key pair and domain certificate. The domain server must store the private key and certificate and provide those objects when processing subsequent requests for this domain. It is also possible to generate a new key pair for a domain in order to roll over the keys. When you roll over the keys for a particular domain, be sure to increment the key version in `generateDomainCredential`.

Each subsequent time that a machine registers with the same domain, the same domain private key and certificate should be used. Invoke `addDomainCredential(DomainToken, PrivateKey)` to return an existing domain credential to the client. If there are multiple domain credentials for the domain because the domain keys were changed, the server should provide domain credentials for the current domain key and all previous domain keys so the client can consume licenses bound to older domain keys. This enables a license bound to an old domain token to be moved to a newly registered machine and still be playable.
