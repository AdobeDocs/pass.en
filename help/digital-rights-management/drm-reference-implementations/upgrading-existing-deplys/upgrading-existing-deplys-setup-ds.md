---
title: Set up a domain server
description: Set up a domain server
copied-description: yes
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
---
# Set up a domain server{#set-up-a-domain-server}

To configure a domain server on an existing license server installation: 

1. In the [!DNL tomcat/lib] directory, open the [!DNL flashaccess-refimpl.properties] file.
1. Under the `Domain CA certificate` option, complete the Domain CA certificate.

   This certificate is then used for accepting the domain tokens.
1. Under the `Domain CA credential` option, complete the `Domain CA credential certificate (PFX)` details.

   This certificate is then used for signing domain certificates and tokens.
1. Specify the value for `DomainServerlURL`.

   If this value is set to `NULL`, the domain authentication may succeed. However, while joining the domain, a join domain error might occur.
