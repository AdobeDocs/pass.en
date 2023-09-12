---
title: About the reference implementations
description: About the reference implementations
copied-description: yes
exl-id: fe387330-9449-4977-be15-069c814354bf
---
# About the reference implementations{#about-the-reference-implementations}

 This guide describes the installation, configuration, and operation of the Adobe Primetime DRM reference implementations. 

>[!NOTE]
>
>Primetime DRM was previously called Adobe Access, and before that, Flash Access.

The Primetime DRM reference implementations include these components:

* **Command line tools** - These tools are based on the same Primetime DRM SDK code used in the Primetime DRM license server. You can perform packaging, licensing, and other DRM tasks from the command line, and alternate seamlessly between using the command-line tools and the license server. 
* **License server** - A fully functional, customizable license server (described below as one of your license server options).

**License Server options:**

* **The Primetime DRM reference implementations** - The subject of this guide, this reference implementation features a robust DRM license server that showcases all of the features provided by the Primetime DRM SDK. This implementation is delivered with source code and instructions for building the code. This implementation is not intended to be used as is (although a [!DNL .war] file is included that you can deploy quickly). It is primarily intended as a reference you can use to build your own custom license server.

  License Server Features:

    * Manages authentication requests by using a database to validate username/password. 
    * Manages license requests and determines the type of license that is being issued when license chaining is applied. 
    * Issues licenses for content that includes multiple Primetime DRM policies. 
    * Issues licenses that support Remote Key delivery to iOS clients, which requires Primetime DRM. 
    * Issues licenses that require an external lookup and retrieval of the Content Encryption Key (CEK). 
    * Searches a database to determine if a user is authorized to view content. 
    * Searches Primetime DRM policy update lists. 
    * Searches machine revocation lists. 
    * Uses an HSM or PKCS12 file to store credentials. 
    * Encrypts passwords that you specified in a properties file. 
    * Specifies multiple license server or transport credentials after the credentials were renewed.

      The old credentials are maintained on the server so users can continue to view existing content without having to repackage. 
    * Restricts DRM/Runtime versions that are allowed to make requests to a license server. 
    * Sets client clock windback preferences. 
    * Restricts the time difference that is allowed between the request time and the server time to prevent replay attacks. 
    * Manages requests from FMRMS 1.x clients

      For example, the FMRMS 1.x client is triggered to upgrade to Primetime DRM 2.0 or later. 
    * Converts FMRMS 1.x metadata to Primetime DRM metadata on demand by using FMRMS 1.x license information that is stored in a database. 
    * Converts FMRMS 1.x policies to Primetime DRM policies for sample code. 
    * Imports FMRMS 1.x license information from an existing database for sample scripts. 
    * Gets the server version 
    * Domain registration 
    * Domain de-registration 
    * Synchronization requests 
    * License Return

* **The Primetime DRM Server for Protected Streaming** - This is a ready-to-go binary that you can implement quickly with minimal effort. It is a good option for customers that want to quickly show Proof of Concept, or it *could* be a production option if your custom DRM needs are minimal. For more information, see Related Information below. 

* **The Primetime Cloud DRM Service** - This is an Adobe-hosted license server that you can use for license serving. (You must be a Primetime licensee to use this service.) This Adobe cloud service relieves you of the expense, maintenance, and engineering required to build your own service. For more information, see Related Information below.
