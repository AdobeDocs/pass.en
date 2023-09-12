---
description: You must ensure that you are securely issuing licenses. Consider these best practices to protect the License Server 
title: Protecting the License Server
exl-id: 88b8f44f-c140-4cbc-be0a-f67058548fc3
---
# Protecting the License Server {#protecting-the-license-server}

You must ensure that you are securely issuing licenses. Consider these best practices to protect the License Server:

## Consuming locally generated CRLs {#consuming-locally-generated-crls}

To consume locally generated certificate revocation lists (CRLs) and policy update lists, use Adobe Primetime DRM APIs to verify the signature.

The following APIs verify that the lists have not been tampered with and that the lists were signed by the correct License Server:

* Call [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) to check the signature before you provide the [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) to any APIs.

  For more information, see [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html). 

* Call [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) to check the signature before providing the `PolicyUpdateList` to any APIs.

  For more information, see [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consuming CRLs published by Adobe{#consuming-crls-published-by-adobe}

The SDK periodically downloads CRLs that are published by Adobe. You must ensure that access to these files is not blocked or the enforcement of these CRLs is not prevented.

The SDK has a configuration option to ignore errors when retrieving Adobe CRLs, and you can only apply this option in development environments. In production environments, the license server must retrieve the CRLs from Adobe. If the license server cannot obtain a valid CRL, an error has occurred.

## Generating CRLs to supplement those published by Adobe{#generating-crls-to-supplement-those-published-by-adobe}

You can use Adobe Primetime DRM to create CRLs that supplement the machine CRL that is published by Adobe.

The Primetime DRM SDK checks and enforces the Adobe CRLs. However, you can disallow additional client machines by creating a CRL that revokes additional machine credentials by passing the CRL to the Primetime DRM SDK. When you issue a license, the SDK checks the Adobe CRL and your CRL.

To generate CRLs, see [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Rollback detection {#rollback-detection}

If your implementation of Adobe Primetime DRM uses business rules that require the client to maintain state (for example, the playback window interval), Adobe recommends that the server keeps track of the rollback counter and use AIR or SWF allow listing.

The rollback counter is sent to the server in most requests from the client. If your implementation of Primetime DRM does not require the rollback counter, it can be ignored. Otherwise, Adobe recommends that the server store the random machine ID, which is obtained using [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), and the current counter value in a database.

For more information on how to increment and track the rollback counter, see [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) and Rollback detection.

## Machine count when issuing licenses {#machine-count-when-issuing-licenses}

If the business rules require that the number of machines for a user be tracked, the License Server or Domain Server must store the machine IDs that are associated with the user.

The most robust way to track machine IDs is to store the value that is returned by the [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) method in a database. When a new request is received, compare the machine ID in the request with the known machine IDs by using [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) performs a comparison of IDs to determine whether the IDs represent the same machine. This comparison is only practical if there is a small number of machine IDs. For example, if users are allowed five machines in their domain, you can search the database for the machine IDs that are associated with the user's username and obtain a small set of data for comparison.

This comparison is not practical for deployments that allow anonymous access. In this case, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) can be used. However, this ID cannot be the same if the user accesses content from Flash and Adobe AIR® runtimes.

>[!NOTE]
>
>The ID does not survive if the user reformats the hard drive.

## Replay protection {#replay-protection}

Replay protection prevents an attacker from replaying a license request message and potentially causing a denial-of-service (DoS) attack against the client.

A DoS attack is an attempt by attackers to prevent legitimate users of a service from using that service. For example, a replay attack that uses the rollback counter could be used to “trick” the License Server into thinking that the DRM client has rolled back its state, which causes a suspension of the account.

To learn more about replay protection, see [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Maintain an allow list of trusted content packagers {#maintain-a-allowlist-of-trusted-content-packagers}

A allow list is a list of trusted entities.

For content packagers, the entities are organizations that are trusted by the content owner to package (or encrypt) the video files and create DRM protected content. When deploying Adobe Primetime DRM, you should maintain an allow list of trusted content packagers. You must also verify the identity of the content packager in the DRM metadata of a DRM protected file before issuing a license.

To learn how to obtain information about the entity that packaged the content, see [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Timeout for authentication tokens{#timeout-for-authentication-tokens}

All authentication tokens that are generated by the Adobe Primetime DRM SDK have a timeout interval to protect application security.

The expiration for the authentication token is specified use the Primetime DRM SDK when handling an authentication request. After it has expired, the token is no longer valid, and the user must authenticate again with the license server.

To learn more about authentication requests, see [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Overriding policy options {#overriding-policy-options}

When you issue a license, the license server can override the usage rules that are specified in the policy.

If the policy specifies a start date, a license is not generated before that start date. However, you can set a future start date in the license after the license has been generated. This option should be used with caution because the client cannot prevent the user from moving the system time forward to circumvent the start date.
