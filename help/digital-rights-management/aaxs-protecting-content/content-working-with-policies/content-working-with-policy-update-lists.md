---
title: Working with Policy Update Lists
description: Working with Policy Update Lists
copied-description: yes
exl-id: 71715eec-e6a3-4640-b17f-ec0c38caf73e
---
# Working with Policy Update Lists{#working-with-policy-update-lists}

For license servers that do not have access to a database for storing information about policies, you may wish to use a policy update list to notify the license server of updated policies. Policy Update Lists may contain updated versions of policies or a list of policy IDs that have been revoked. If a policy update list is supplied in `HandlerConfiguration`, the SDK will enforce this list when issuing a license.

Policies may also be revoked if content owners or distributors want to discontinue issuing licenses under a particular policy. A policy update list may be used to enforce policy revocation in the SDK. Policy update lists may also be used to provide a list of updated policies to the SDK. Note that revoking a policy does not revoke licenses that have already been issued. It only prevents additional licenses from being issued under that policy.

Working with policy update lists involves the use of a `PolicyUpdateListFactory` object. To create a policy update list, load an existing policy update list, and check whether a policy has been updated or revoked by using the Java API, perform the following steps:

1. Set up your development environment and include all of the JAR files mentioned in Setting up the development environment within your project. 
1. Create a `ServerCredentialFactory` instance to load the credentials needed for signing. 
1. Create a `PolicyUpdateListFactory` instance using the `ServerCredential` you created. 
1. Specify the policy ID to be revoked. 
1. Create a `PolicyRevocationEntry` object using the policy ID `String` you just created, and add it to the policy update list by passing it into `PolicyUpdateListFactory.addRevocationEntry()`. Generate the new policy update list by calling `PolicyUpdateListFactory.generatePolicyUpdateList()`. Similarly, updated policies can be added to the list using `PolicyUpdateEntry`. 
1. If a policy update list already exists, you can serialize it for loading by calling `PolicyUpdateList.getBytes()`. To load the list, call `PolicyUpdateListFactory.loadPolicyUpdateList()` and pass in the serialized list. 
1. Verify the signature is valid and the list was signed by the correct license server certificate by calling `PolicyUpdateList.verifySignature()`. 
1. To check whether an entry was revoked, pass the policy ID `String` into `PolicyUpdateList.isRevoked()`. Alternatively, the list can be passed into `HandlerConfiguration` and it will be enforced when licenses are issued.

To add additional entries to an existing `PolicyUpdateList`, load an existing policy update list. Create a new `PolicyUpdateListFactory` instance. Call P `olicyUpdateListFactory.addEntries` to add all the entries from the old list to the new list. Call `PolicyUpdateListFactory.addRevocationEntry` or `addUpdatedEntry` to add any new revocation or update entries to the PolicyUpdateList.

For sample code demonstrating how to create a policy update list, load an existing policy update list, and check whether a policy has been revoked, see `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` in the Reference Implementation Command Line Tools “samples” directory.
