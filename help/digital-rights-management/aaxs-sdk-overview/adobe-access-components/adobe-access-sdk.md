---
description: The main components of Adobe Access consist of a Java SDK, and the Flash Player and Adobe AIR client runtime environments.
title: Java SDK, Flash Player and Adobe AIR client
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
---
# Adobe Access components{#adobe-access-components}

The main components of Adobe Access consist of a Java SDK, and the Flash Player and Adobe AIR client runtime environments.

For more information on setting up the SDK, see Setting up the SDK in *Using the Adobe Access SDK for Protecting Content.*

The Adobe Access SDK lets you develop a digital rights management solution that integrates with your organization's existing business infrastructure, such as content management, billing, and user access control systems. Flash Player and Adobe AIR let you create and easily deploy applications through which consumers can access and view large libraries of digital content.

## Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access is delivered as a Java SDK that provides the building blocks from which you can create a server implementation. Using the SDK you can create an Adobe Access solution suited to your organization's business model.

The Java APIs provided in the SDK are described in the following sub-sections.

## Java APIs for managing device group domains {#java-apis-for-managing-device-group-domains}

These APIs are used to allow the server to handle client requests for joining and leaving device group domains.

A device group domain is a logical collection of devices that are able to share licenses between each other. In order for this to happen, each device must first join/register to the same domain. The Adobe Access SDK, running on a server, must handle the Device Domain join (register) requests, as well as Device Domain leave (de-register) requests. Devices that are not joined to any domain will be issued licenses that are bound to that device, which cannot be shared to any other device.

## Java APIs for protecting content {#java-apis-for-protecting-content}

These APIs are used to define rights and prepare content for distribution. The content protection APIs are:

* Policy management

  The policy management API is used to create and modify policies to be applied to content. Policies can be created or updated, including getting/setting all usage rules and allowing additional parameters in a custom namespace. 

* Content packaging

  The content packaging API is used to encrypt content and retrieve metadata from the packaged content.

## Java APIs for issuing licenses {#java-apis-for-issuing-licenses}

These APIs are used when a client requests a license from the server. The SDK supports the following requests from the client:

* Authentication

  The authentication API can be used to handle authentication requests and generate authentication tokens. 

* License generation and acquisition

  The license generation and acquisition API is used to generate a license for the user. 

* Support for Adobe AIR version 1.5 clients and content

  For the purposes of backwards compatibility, the SDK has APIs to handle requests from AIR applications created for use with AIR version 1.5 and earlier clients and protected content.

## Reference implementation {#reference-implementation}

The SDK includes a reference implementation, a simple Adobe Access deployment that demonstrates how to use the Java APIs. The reference implementation provides a License Server, Watched Folder Packager, Adobe Access Manager AIR application, and command line tools for content packaging and policy management based on the Java APIs. To learn more about the Adobe Access reference implementation, see *Protecting Content*.

## Adobe Access Server for Protected Streaming {#adobe-access-server-for-protected-streaming}

For streaming use cases where content is protected with Adobe Access, such as for Adobe HTTP Dynamic Streaming, the software also includes Adobe Access Server for Protected Streaming. This solution can be easily deployed on a servlet container such as Tomcat and can achieve a high level of scalability and performance to meet the largest content distribution needs.

## Adobe Flash Player {#adobe-flash-player}

 Flash Player is a lightweight browser plug-in and runtime that delivers consistent and engaging user experiences, stunning audio/video playback, and pervasive reach. Flash Player provides high-quality playback of streamed or downloaded video content. For content publishers, Flash Player provides the means to customize the playback screens surrounding content, allowing deeper branding experiences and monetization through advertising using banners and overlays. For consumers, Flash Player presents an intuitive and visually appealing way to view video content.

For more information on Flash Player, visit: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR is a cross-operating system runtime that allows content producers to extend their existing investments in the web to the desktop by designing customized multimedia applications. Built on proven, open technologies, it provides a reliable, simplified way for businesses to develop and deploy custom applications that can be trusted to deliver a more secure, enjoyable user experience. Adobe AIR allows businesses to easily integrate rich media to create a more immersive and interactive user experience. It lets developers use familiar tools such as HTML, JavaScript, Flash, or Adobe&reg; Flex&reg; software to deploy their unique combination of rich Internet applications to either Windows, Macintosh, or Linux.

Businesses have complete control of the user interface, and they can design a user experience to reflect and reinforce their brand. With built-in support for playback of content protected with Adobe Access SDK, Adobe AIR helps create custom, end-to-end content distribution chains.

## Native iOS and Android Applications {#native-ios-and-android-applications}

Native iOS and Android Applications Available only to Adobe Primetime customers, Adobe Access DRM 4.0 and higher can be used to protect video that is consumed within native (non-Flash) applications on mobile devices. In order for an application to consume this protected content, it must be implemented using the Adobe Primetime Client libraries.

For more information on Adobe Primetime, visit: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
