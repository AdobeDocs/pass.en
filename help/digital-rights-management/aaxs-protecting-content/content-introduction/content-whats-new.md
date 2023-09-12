---
description: Adobe® Access™ is an advanced digital rights management and content protection solution for high-value audiovisual content. Using tools that you create using Java APIs, you can create policies, apply policies to files containing audio and video content, and encrypt those files. The high-level steps for performing these tasks are as follows 
title: Overview
exl-id: cf081058-9b41-4b09-9258-a7d873799846
---
# Overview {#overview}

Adobe® Access™ is an advanced digital rights management and content protection solution for high-value audiovisual content. Using tools that you create using Java APIs, you can create policies, apply policies to files containing audio and video content, and encrypt those files. The high-level steps for performing these tasks are as follows:

1. Use the Java APIs to set the policy properties and encryption parameters. 
1. Create a policy describing the usage roles for the content. (See [Working with policies](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   You can create any number of policies. Most users create a small number of policies and apply them to many files. 

1. Package a media file.

   In this context, *packaging a file* means to encrypt it and apply a policy to it. (See [Packaging media files](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).) 

1. Implement the license server to issue a license to the user.

The encrypted content is now ready for deployment, and the client can request the license from the server.

The SDK provides a Java API to accomplish these tasks, and includes reference implementations of the license server, and command line tools that are based on the Java APIs. For information, see *Using the Adobe Access Reference Implementations*.

## What is new in Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **External CEK**: The ability to integrate a Content Key Management System (CKMS) to the DRM license serving and Content Packaging workflows, instead of encrypting the CEK and bundling it into the content's metadata. See [Adobe Access DRM External CEK Overview](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md). 

* **License (voucher) Return**: The ability for a client to return (or delete) a license issued to the client. 
* **Xbox Key Server**: The ability to protect content sent to the Xbox and Xbox 360. (An Adobe Primetime client is required.)

## Custom usage rules {#custom-usage-rules}

Specifies custom usage rules. Custom data can be included in licenses issued by the License Server. The interpretation/handling of this data is completely up to the implementation of the client application and license server.

Example use case: Enables extensibility of usage rules by allowing other business rules to be conveyed securely as part of the policy and/or content license. For security reasons, because these usage rules are enforced in custom client application code, this option should be used in conjunction with the AIR application or Flash Player SWF allow list options. For more information, see [Runtime and application restrictions](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
