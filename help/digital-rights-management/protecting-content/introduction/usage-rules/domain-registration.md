---
title: Device Group Domain Registration
description: Device Group Domain Registration
copied-description: yes
exl-id: 81d6023b-76e0-4786-805b-bfe77e9f8513
---
# Device Group Domain Registration{#device-group-domain-registration}

As an alternative to binding a license to a specific device, Primetime DRM 3.0 or later supports binding licenses to a device domain.

Multiple devices may join a domain and receive domain tokens. After a device in the domain acquires a license, the license may be transferred to any other device in the domain, and those devices can play the content without acquiring a license directly from the license server.

If you want to support any domain-bound licenses, then the Primetime DRM policy must specify the domain server with which the client must register. The Primetime DRM policy must also specify the authentication requirements for the domain server whether anonymous access is enabled or whether the server requires username/password or custom authentication.

Domain registration and domain-bound licenses are supported by Primetime DRM clients version 3.0 or later. If an older client or an Adobe Primetime 3.0 client in Flash Player requests a license for content that supports domain registration, the license server may issue a license that uses an alternative Primetime DRM policy to support binding to a specific device.
