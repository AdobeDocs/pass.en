---
title: Handling Domain De-Registration requests
description: Handling Domain De-Registration requests
copied-description: yes
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
---
# Handling Domain De-Registration requests{#handling-domain-de-registration-requests}

If the client application needs to leave a domain, it invokes the `DRMManager.removeFromDeviceGroup()`ActionScript API or the `leaveLicenseDomain()` iOS API to initiate the domain de-registration process. Domain de-registration is a two phase process. The client first sends a de-registration preview request. The domain server examines the request and determines whether the client is permitted to leave the domain (an error may be returned if the machine is not currently part of the domain). Upon a successful response, the client deletes its domain credentials and any licenses issued to that domain, then sends a de-registration request.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "Domain Server URL in metadata: + "/flashaccess/dereg/v4". Otherwise, the request URL is Domain Server URL in metadata” + “/flashaccess/dereg/v3”

When processing domain de-registration requests, the server uses `getRequestPhase()` to determine whether the client is in the preview or de-registration phase. In the preview phase, the domain server examines the request and determines whether the client is permitted to leave the domain (the request may be denied, for example, if the machine is not currently part of the domain). In the de-registration phase, the server records the fact that the machine has left the domain. The server is highly recommended to evaluate the same logic in the preview request as in the actual de-registration request to minimize the chance of the second phase failing.
