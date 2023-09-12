---
title: Ensure compatibility with Flash Media Rights Management Server 1.x
description: Ensure compatibility with Flash Media Rights Management Server 1.x
copied-description: yes
exl-id: 324ea561-c666-4cf9-871b-11f6b6b406f1
---
# Ensure compatibility with Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x and Adobe Access use different metadata for packaging content and requesting licenses. For Adobe Access to use FMRMS version 1.x content, the metadata must be converted.

The Adobe Access SDK supports two options for converting metadata:

* Offline (recommended)

  Generate the Adobe Access metadata in an offline process and store it for use when a client requests it. Adobe recommends this option. If metadata is generated offline, the license server does not need access to the 1.x CEKs or the packager credential. In addition, converting offline offers better performance because the License Server doesn't need to generate the metadata in real time. 

* On-demand

  Generate the Adobe Access metadata on-demand when a client requests it. When an Adobe Access client downloads version 1.x content, it sends the DRM metadata (also known as the DRM header) to the Adobe Access SDK. The SDK converts the DRM metadata to the current format. The SDK encrypts and embeds the content encryption key (CEK) in the metadata and sends the content back to the Adobe Access client. (The Adobe Access 1.x metadata does not contain the CEK.)

  To convert the metadata, Adobe Access requires access to the Adobe Access 1.x content encryption keys. When you migrate from Flash Media Rights Management Server 1.x, you can continue to store the content encryption keys in the LiveCycle ES database, or you can implement a custom solution to securely store the content encryption keys elsewhere. If you choose to continue storing the content encryption keys in the LiveCycle ES database, follow the recommendations outlined in "Protecting access to sensitive content in the database" in *Hardening and Security for LiveCycle ES*.

For more information on ensuring compatibility with content packaged using Flash Media Rights Management Server 1.x, see the *Adobe Access API Reference*.
