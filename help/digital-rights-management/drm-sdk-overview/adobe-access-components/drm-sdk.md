---
description: The main components of Primetime DRM consist of a Java SDK, and the Flash Player and Adobe AIR client runtime environments.
title: Java SDK, Flash Player and Adobe AIR client
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
---
# Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM is delivered as a Java SDK that provides the building blocks from which you can create a server implementation. Using the SDK you can create an Primetime DRM solution suited to your organization's business model.

The Java APIs provided in the SDK are described in the following sub-sections. 

## Java APIs for managing device group domains{#java-apis-for-managing-device-group-domains}

These APIs are used to allow the server to handle client requests for joining and leaving device group domains.

A device group domain is a logical collection of devices that are able to share licenses between each other. In order for this to happen, each device must first join/register to the same domain. The Primetime DRM SDK, running on a server, must handle the Device Domain join (register) requests, as well as Device Domain leave (de-register) requests. Devices that are not joined to any domain will be issued licenses that are bound to that device, which cannot be shared to any other device.

## Java APIs for protecting content{#java-apis-for-protecting-content}

These APIs are used to define rights and prepare content for distribution. The content protection APIs are:

* Policy management

  The policy management API is used to create and modify policies to be applied to content. Policies can be created or updated, including getting/setting all usage rules and allowing additional parameters in a custom namespace. 

* Content packaging

  The content packaging API is used to encrypt content and retrieve metadata from the packaged content.

## Java APIs for issuing licenses{#java-apis-for-issuing-licenses}

These APIs are used when a client requests a license from the server. The SDK supports the following requests from the client:

* Authentication

  The authentication API can be used to handle authentication requests and generate authentication tokens. 

* License generation and acquisition

  The license generation and acquisition API is used to generate a license for the user. 

* Support for Adobe AIR version 1.5 clients and content

  For the purposes of backwards compatibility, the SDK has APIs to handle requests from AIR applications created for use with AIR version 1.5 and earlier clients and protected content.

## Reference implementation {#reference-implementation}

The SDK includes a reference implementation, a simple Adobe Primetime DRM deployment that demonstrates how to use the Java APIs. The reference implementation provides a License Server, Watched Folder Packager, Primetime DRM Manager AIR application, and command line tools for content packaging and policy management based on the Java APIs. To learn more about the Primetime DRM reference implementation, see Protecting Content.
