---
title: Revoking machine credentials
description: Revoking machine credentials
copied-description: yes
exl-id: 6dffcb1f-3e9b-423c-800a-90075afe779b
---
# Revoking machine credentials{#revoking-machine-credentials}

Adobe maintains a CRL for revoking machine credentials that are known to be compromised. This CRL is automatically enforced by the SDK. If there are additional machines to which you do not want your license server to issue licenses, you may create a machine revocation list and add the issuer name and serial number of the machine tokens you want to exclude (use `MachineToken.getMachineTokenId()` to retrieve the issuer name and serial number of the machine certificate).

Revoking machine credentials involves the usage of a `RevocationListFactory` object. To create a revocation list, load an existing revocation list, and check whether a machine token has been revoked by using the Java API, perform the following steps:

1. Set up your development environment and include all of the JAR files mentioned in [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) within your project. 
1. Create a `ServerCredentialFactory` instance to load the credentials needed for signing. The license server credential is used to sign the revocation list. 
1. Create a `RevocationListFactory` instance. 
1. Specify the issuer and serial number of the machine token to be revoked by using a `IssuerAndSerialNumber` object. All Adobe Access requests contain a machine token. 
1. Create a `RevocationList` object using the `IssuerAndSerialNumber` object you just created, and add it to the revocation list by passing it into `RevocationListFactory.addRevocationEntry()`. Generate the new revocation list by calling `RevocationListFactory.generateRevocationList()`. 
1. To save the revocation list, you can serialize it by calling `RevocationList.getBytes()`. To load the list, call `RevocationListFactory.loadRevocationList()` and pass in the serialized list. 
1. Verify that the signature is valid and the list was signed by the correct license server by calling `RevocationList.verifySignature()`. 
1. To check whether an entry was revoked, pass the `IssuerAndSerialNumber` object into `RevocationList.isRevoked()`. The revocation list may also be passed into `HandlerConfiguration` to have the SDK enforce the revocation list for all authentication and license requests.

To add additional entries to an existing `RevocationList`, load an existing revocation list. Create a new `RevocationListFactory` instance, and be sure to increment the CRL number. Call `RevocationListFactioryEntries.addRevocationEntries` to add all the entries from the old list to the new list. Call `RevocationListFactory.addRevocationEntry` to add any new revocation entries to the RevocationList.

For sample code demonstrating how to create a revocation list, load an existing revocation list, and check whether a machine token has been revoked, see `com.adobe.flashaccess.samples.revocation.CreateRevocationList` in the Reference Implementation Command Line Tools “samples” directory.
