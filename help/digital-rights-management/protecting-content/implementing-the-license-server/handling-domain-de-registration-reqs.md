---
title: Handle Domain De-Registration requests
description: Handle Domain De-Registration requests
copied-description: yes
exl-id: 14b97ba2-9344-4d84-8c52-f33126337454
---
# Handle Domain De-Registration requests {#handle-domain-de-registration-requests}

If the client application needs to leave a domain, it invokes the `DRMManager.removeFromDeviceGroup()`ActionScript API or the `leaveLicenseDomain()` iOS API to initiate the domain de-registration process. Domain de-registration is a two phase process. The client first sends a de-registration preview request. The domain server examines the request and determines whether the client is permitted to leave the domain. An error may be returned if the machine is not currently part of the domain. Upon a successful response, the client deletes its domain credentials and any licenses that have been issued to that domain. It then sends a de-registration request.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "Domain Server URL in metadata: + " [!DNL /flashaccess/dereg/v4]". Otherwise, the request URL is Domain Server URL in metadata” + " [!DNL /flashaccess/dereg/v3]"

When processing domain de-registration requests, the server uses `getRequestPhase()` to determine whether the client is in the preview or de-registration phase. In the preview phase, the domain server examines the request and determines whether the client is permitted to leave the domain because the request may be denied; for example, the request may be denied if the machine is not currently part of the domain. In the de-registration phase, the server records the fact that the machine has left the domain. The server is highly recommended to evaluate the same logic in the preview request as in the actual de-registration request to minimize the chance of the second phase failing.
