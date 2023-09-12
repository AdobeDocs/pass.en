---
title: Working with DRM policies overview
description: Working with DRM policies overview
copied-description: yes
exl-id: 734d0be3-2abe-400c-bc34-00046ec52f4c
---
# Overview {#working-with-drm-policies-overview}

Content providers can apply DRM policies to media files using the Primetime DRM SDK. Administrators can then create, view details of, and update DRM policies using policy management APIs.

A *`DRM policy`* is a collection of information that includes security settings, authentication requirements, and usage rights. The policy defines how users can view content. DRM policies, encryption, and signing allow content providers to maintain control of their content no matter how widely the content is distributed.

A DRM policy serves as a template that the license server uses when it generates a license. A client may also refer to the DRM policy before it requests a license, to determine whether the client needs to prompt the user for authentication before it issues a license request to the server.

You can deliver protected content using Adobe Flash Media Server or an HTTP server. Users can download and play protected content in custom players built with the Primetime DRM SDK.

A DRM policy specifies one or more rights that are granted to the client. Typically, a DRM policy includes, at a minimum, the *`Play Right`*. You can also specify multiple Play Rights, each with different restrictions. When the client receives a license with multiple Play Rights, it uses the first license that meets all the restrictions. For example, you could enforce different output protection settings on different platforms.

See `CreatePolicyWithOutputProtection.java` in the Reference Implementation Command Line Tools [!DNL samples] directory for sample code that illustrates this example.

You can complete the following tasks with the Primetime DRM policy management APIs:

* Create and update policies 
* View DRM policy details 
* Manage DRM policy update lists

See the *Primetime DRM API Reference* for details about the Java API.

See the *Using the Primetime DRM Reference Implementations* guide for information about the Primetime DRM Policy Manager.
