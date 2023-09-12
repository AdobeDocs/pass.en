---
title: License Server deployment options
description: License Server deployment options
copied-description: yes
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
---
# License Server deployment options{#license-server-deployment-options}

The License Server can be deployed using one of the following options:

* **Adobe Access Server for Protected Streaming** -- This License Server is optimized for streaming. For instance, you can set up the server for Adobe HTTP Dynamic Streaming with Adobe Access. This server can be deployed easily with very little configuration required and will support multiple tenants, and can achieve a high level of scalability. However, since this implementation is optimized for streaming, it does not support the full Adobe Access features. For instance, username/password authentication, domains, and license chaining are not supported. The usage rules in licenses issued by this server are controlled through a server configuration file, which overrides the policy used at packaging time. See the *Adobe Access Server for Protected Streaming Guide* for more details on the usage rules supported by this server. 
* **Reference Implementation License Server** -- Use this setup as a starting point for a custom server implementation. This is an example license server implementation, including source code, which demonstrates how to use the APIs in the Adobe Access SDK to handle all types of requests and how to implement custom business logic backed by a database. The usage rules in licenses issued by this server are controlled through the policy associated with the content at packaging time. 
* **Custom Server Implementation** -- You can also implement your own licensing server using the SDK. The information in this chapter describes the APIs used to implement a license server.
