---
title: Custom metadata
description: Custom metadata
copied-description: yes
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
---
# Custom metadata {#custom-metadata}

Use this to add custom key/value pairs to content metadata that can be interpreted by the server application.

The metadata format for Primetime DRM content enables you to include custom key/value pairs at packaging time. This custom metadata can then be processed by the license server during license issuance. The metadata is separate from a Primetime DRM policy, and can be unique for each section of content.

Example use case: During a Beta phase, you can include the custom property `Release:BETA` at packaging time. License servers can vend licenses to this content during the Beta period. However, after the Beta period expires, the license servers disallow access to the content.
