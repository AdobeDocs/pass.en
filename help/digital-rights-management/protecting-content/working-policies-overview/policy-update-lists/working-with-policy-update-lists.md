---
title: Working with DRM Policy Update Lists
description: Working with DRM Policy Update Lists
copied-description: yes
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
---
# DRM policy update lists {#drm-policy-update-lists}

If you update the usage rules in a DRM policy after packaging any content, the license server needs to have the latest version before it can issue licenses that use an updated DRM policy. One way to achieve this is through a DRM policy update list.

A DRM policy update list is represented by a file that includes a list of updated or revoked DRM policies. Whenever you update a DRM policy, you need to generate a new DRM Policy Update List and periodically push the list to all license servers.

## Working with DRM Policy Update Lists {#working-with-drm-policy-update-lists}

For license servers that do not have access to a database for storing information about DRM policies, you may want to use a DRM policy update list to notify the license server of any updated DRM policies. DRM Policy Update Lists may include updated versions of DRM policies or a list of DRM policy IDs that have been revoked. If a policy update list is included in `HandlerConfiguration`, the SDK enforces this list when it issues a license.

You can also revoke any DRM policies if content owners or distributors want to discontinue issuing licenses under a particular DRM policy. A DRM policy update list can be used to enforce DRM policy revocation in the SDK. You can also apply DRM policy update lists to provide a list of updated DRM policies to the SDK.

>[!NOTE]
>
>Whenever you revoke a DRM policy, any licenses that have already been issued are not automatically revoked. It only prevents additional licenses from being issued under that DRM policy.

## Update Policy Update Lists{#update-policy-update-lists}

Working with DRM policy update lists involves the use of a `PolicyUpdateListFactory` object. If you want to create a DRM policy update list, you need to load an existing DRM policy update list, and then check whether a DRM policy has been updated or revoked by using the Java API.

To work with DRM Policy Update Lists: 

1. Set up your development environment and include all of the JAR files that are included when you set up the development environment in a project .
1. Create a `ServerCredentialFactory` instance to load the credentials that are needed for signing.
1. Create a `PolicyUpdateListFactory` instance by using the `ServerCredential` that you created.
1. Specify the DRM policy ID that you want to revoke.
1. Create a `PolicyRevocationEntry` object by using the DRM policy ID `String` that you just created, and then add it to the DRM policy update list by passing it into `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generate the new DRM policy update list by calling `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Similarly, you can update DRM policies to the list by using `PolicyUpdateEntry`.
1. If a DRM policy update list already exists, you can serialize it for loading by calling `PolicyUpdateList.getBytes()`.

   To load the list, call `PolicyUpdateListFactory.loadPolicyUpdateList()` and pass it in the serialized list.
1. Verify that the signature is valid and the list has been signed by the correct license server certificate by calling `PolicyUpdateList.verifySignature()`.
1. Pass the DRM policy ID `String` into `PolicyUpdateList.isRevoked()` to verify that an entry has been revoked.

   Alternatively, you can pass the list to `HandlerConfiguration` where it is then enforced whenever licenses are issued.
If you want to add more entries to an existing `PolicyUpdateList`, you need to load an existing DRM policy update list. Therefore you need to create a new DRM `PolicyUpdateListFactory` instance. Call `PolicyUpdateListFactory.addEntries` to add all the entries from the old list to the new list. Call `PolicyUpdateListFactory.addRevocationEntry` or `addUpdatedEntry` to add any new revocation or update entries to the DRM PolicyUpdateList.

For sample code that demonstrates how to create a DRM policy update list, see `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` in the *Reference Implementation Command Line Tools* [!DNL samples] directory.
