---
title: Software Requirements
description: Software Requirements
copied-description: yes
exl-id: aa2ae6ac-7c2a-4cc3-a3a4-b7f92e478d23
---
# Software Requirements {#software-requirements}

* Tomcat 6
* JDK 1.8

## Code Delivery / Package Contents{#code-delivery-package-contents}

The Adobe Primetime DRM On Premises Individualization Server package contains the following:

* [!DNL flashaccess.war] - The Individualization Server 
* [!DNL flashaccess-kgs.war] - The optional Key Generation Server 
* [!DNL /shared] - Contains:

    * [!DNL adobe-flashaccess-certs.jar] 
    * [!DNL AdobeInitial.properties] - Sample properties file

* [!DNL thirdparty/] - Includes Crypto-J support as native libraries:

    * [!DNL libjsafe.so] (Linux) 
    * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - A utility for encrypting server credential passwords 
* [!DNL ROOT] - contains a [!DNL crossdomain.xml] file 

* ECI cache files - Pre-downloaded 
* [!DNL addIndivCert.py] - A script for updating a License Server's root of trust to support On Premises individualizations 
* [!DNL CreateMetadata.jar] - A utility for creating On Premises DRM Metadata 
* [!DNL client_sample/] - A folder with a client code snippet 
* Release Notes - For any last minute additions to the documentation

## Obtain Individualization Server Certificates{#obtain-individualization-server-certificates}

To use the On Premises Individualization Server, you must first obtain two digital credentials (certificates):

* *Individualization Transport Credential* - issued by Adobe 
* *Individualization CA Credential* - issued by Symantec (VeriSign)

To obtain these certificates, submit a request via Zendesk ticket to: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Please note that these credentials are in addition to the credentials required for operating a Primetime DRM License Server.
