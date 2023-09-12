---
title: Client Integration
description: Client Integration
copied-description: yes
exl-id: 7326eb86-c407-4422-bf74-d6b6e17bbf3e
---
# Client Integration{#client-integration}

In order to direct the client into individualizing against the On Premises Individualization server (as opposed to the Adobe Hosted Global Individualization Server), the client should utilize the previously created On Premises DRM Metadata. Having an un-individualized client perform a license acquisition or initialize DRM, using the special metadata, will result in the client connecting to the custom Individualization Server URL.

A sample code snippet is included in the [!DNL client_sample] folder.
