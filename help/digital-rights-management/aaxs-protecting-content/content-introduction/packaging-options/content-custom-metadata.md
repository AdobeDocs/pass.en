---
title: Custom metadata
description: Custom metadata
copied-description: yes
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
---
# Custom metadata {#custom-metadata}

**Specify custom key/value to add to content metadata that can be interpreted by the server application.**

The Adobe Access content metadata format allows for inclusion of custom key/value pairs at packaging time to be processed by the license server during license issuance. This metadata is separate from the policy and can be unique for each piece of content.

Example use case: During a Beta phase, you include the custom property "Release:BETA" at packaging time. License servers can vend licenses to this content during the Beta period, but after the Beta period expires, the license servers disallow access to the content.
