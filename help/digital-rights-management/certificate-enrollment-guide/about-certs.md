---
title: About certificates
description: About certificates
copied-description: yes
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
---
# About certificates {#about-certificates}

The Adobe Primetime DRM SDK is available in the following configurations:

* Primetime DRM Production SDK 
* Primetime DRM Evaluation SDK 
* Primetime DRM Trial SDK

To use the Primetime DRM SDK to create a licensing server, you must obtain digital certificates from Adobe. Digital certificates (also referred to simply as certificates) bind an entity, such as an individual, organization, or system, to a specific public and private key pair. Digital certificates can be thought of as electronic credentials that verify the identity of an individual, system, or organization.

To allow maximum flexibility and enhanced security in your deployment options, the Primetime DRM SDK requires four certificates:

* License Server certificate

  The SDK uses this certificate to sign content licenses issued to clients. 
* Packager certificate

  The SDK uses this certificate to generate DRM metadata when packaging (encrypting) content. 
* Transport certificate

  The SDK uses this certificate to secure the communication between the clients and license server. 
* Domain CA certificate

  Customers who want to implement a domain server need the Domain CA certificate. Unlike the other certificates, the Domain CA certificate is not issued by Adobe.

>[!NOTE]
>
>For the Evaluation SDK and the Trial SDK, the License Server, Packager, and Transport certificates are combined into a single certificate.
