---
title: License Server deployment options
description: License Server deployment options
copied-description: yes
exl-id: e06d59c0-517d-4483-9132-ceb37efada31
---
# License Server deployment options{#license-server-deployment-options}

You can deploy the License Server by using one of the following options:

* Adobe Primetime DRM Server for Protected Streaming—This License Server is optimized for streaming. For instance, you can set up the server for Adobe HTTP Dynamic Streaming with Primetime DRM. This server can be deployed easily with very little configuration required and supports multiple tenants. It can achieve a high level of scalability. Because this implementation is optimized for streaming, it does not support the full Primetime DRM features. For instance, username/password authentication, domains, and license chaining are not supported. The usage rules in licenses issued by this server are controlled through a server configuration file, which overrides the policy used at packaging time.

  See the *Adobe Primetime DRM Server for Protected Streaming Guide* for more details about the usage rules that are supported by the License server. 
* Reference Implementation License Server—You can use this setup to customize your server implementation. This is an example license server implementation, including source code, which demonstrates how to use the APIs in the Primetime DRM SDK to manage all types of requests and how to implement custom business logic backed by a database. The usage rules in licenses issued by this server are controlled through the policy associated with the content at packaging time. 
* Custom Server Implementation—You can also implement your own licensing server with the SDK. The information describes how the APIs are used to implement a license server.
