---
title: License server and watched folder packager overview
description: License server and watched folder packager overview
copied-description: yes
exl-id: 1a355068-7ad6-4cc2-8447-49251dae3ff8
---
# License server and watched folder packager overview {#license-server-and-watched-folder-packager-overview}

The reference implementation server can help you create a license server using the Adobe Access SDK. In this implementation, users are authenticated based on user entries in a database. The server includes demonstration business logic for issuing licenses. It also implements compatibility support for Flash Media Rights Management Server 1.0 and 1.5.

The reference implementation server also includes a watched folder implementation of the packager. This component may be deployed along with the license server or on a separate machine. With this packager implementation, multiple watched folders can be created. When content is dropped into the watched folder, the packager automatically packages the content.

The license server and packager are deployed as separate WAR files, so you can choose whether to run them on separate servers or in a single Apache Tomcat® instance. The license server is in the [!DNL flashaccess.war] and the packager is in [!DNL flashaccess-packager.war]. The optional [!DNL edcws.war] contains support for license requests from FMRMS 1.x clients.

The Reference Implementation sample code demonstrates the following features:

* License Server:

    * Handling authentication requests, using a database to validate username/password 
    * Handling license requests and determining which type of license to issue when license chaining is used. 
    * Issuing licenses for content containing multiple policies 
    * Issue licenses that support Remote Key delivery to iOS clients (requires Adobe Primetime) 
    * Issuing licenses that require an external lookup/retrieval of the Content Encryption Key (CEK) 
    * Using database to determine if user is authorized to view content 
    * Using policy update lists 
    * Using machine revocation lists 
    * Using an HSM or PKCS12 file to store credentials 
    * Encrypting passwords specified in properties file 
    * Specifying multiple license server or transport credentials (after credentials are renewed, the old credentials are kept on the server so existing content can be consumed without needing to repackage) 
    * Restricting DRM/Runtime versions allowed to make requests to the license server 
    * Setting client clock windback preferences 
    * Restricting time difference allowed between request time and server time (to prevent replay attacks) 
    * Handling requests from FMRMS 1.x clients (triggers FMRMS 1.x client to upgrade to Adobe Access 2.0 or later) 
    * Converting FMRMS 1.x metadata to Adobe Access metadata on the fly, using FMRMS 1.x license information stored in a database 
    * Sample code for converting FMRMS 1.x policies to Adobe Access policies 
    * Sample scripts for importing FMRMS 1.x license information from an existing database 
    * Get Server Version 
    * Domain registration 
    * Domain de-registration 
    * Synchronization requests 
    * License Return

* Packager Server:

    * Implementing a packager implementation that automatically packages content added to a watched folder 
    * Using an HSM or PKCS12 file to store credentials 
    * Encrypting passwords specified in properties file 
    * Configuring the packager, creating policies, and creating policy update lists using an AIR application
