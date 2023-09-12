---
title: Device Group Domain Registration
description: Device Group Domain Registration
copied-description: yes
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
---
# Device Group Domain Registration{#device-group-domain-registration}

As an alternative to binding a license to a specific device, Adobe Access 3.0 and higher supports binding licenses to a device domain. Multiple devices may join a domain and receive domain tokens. After a device in the domain acquires a license, the license may be transferred to any other device in the domain, and those devices can play the content without acquiring a license directly from the license server.

To support the domain-bound licenses, the policy must specify the domain server with which the client must register. The policy will also specify the authentication requirements for the domain server (whether anonymous access is allowed or whether the server requires username/password or custom authentication).

Domain registration and domain-bound licenses are supported by Adobe Access clients version 3.0 and higher. If an older client or a Adobe Access 3.0 client in Flash Player requests a license for content that supports domain registration, the license server may issue a license using an alternative policy that supports binding to a specific device.
