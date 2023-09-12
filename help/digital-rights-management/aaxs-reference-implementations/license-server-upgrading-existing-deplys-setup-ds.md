---
title: Set up a domain server
description: Set up a domain server
copied-description: yes
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
---
# Set up a domain server {#set-up-a-domain-server}

To configure the domain server on an existing license server installation, perform the following tasks:

1. Open the [!DNL flashaccess-refimpl.properties] file under [!DNL tomcat/lib]. 

1. Under the `Domain CA certificate` option, fill the Domain CA certificate details. This certificate will be used for accepting the domain tokens. 
1. Under the `Domain CA credential` option, fill in the `Domain CA credential certificate (PFX)` details. This certificate will be used for signing domain certificates and tokens. 

1. Specify the value for `DomainServerlURL`. If this value is NULL, the domain authentication may succeed. However, while joining the domain, there will be a join domain error.
