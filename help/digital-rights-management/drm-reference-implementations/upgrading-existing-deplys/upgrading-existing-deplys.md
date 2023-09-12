---
description: To upgrade a server that supports the version 3.0 Reference Implementation License Server or Watched Folder Packager, you need to replace the .war files that have been deployed on an Application Server with the files that have been included with Adobe Primetime DRM Reference Implementation Server.
title: Upgrade existing deployments
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
---
# Overview {#upgrade-existing-deployments-overview}

To upgrade a server that supports the version 3.0 Reference Implementation License Server or Watched Folder Packager, you need to replace the .war files that have been deployed on an Application Server with the files that have been included with Adobe Primetime DRM Reference Implementation Server.

To use domain registration with the Reference Implementation License Server, several new database tables are required. You need to recreate the entire reference implementation database and run `CreateSampleDB.sql`.

To preserve database records and add new tables:

1. Open `CreateSampleDB.sql` and run commands that create the following tables:

    * `DomainServerInfo` 
    * `DomainKeys` 
    * `DomainMembership` 
    * `UserDomainMembership` 
    * `UserDomainRefCount`

1. Add the following properties to [!DNL flashaccess-refimpl.properties] to use the domain support:

    * `HandlerConfiguration.DomainCAs.n` or `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n` 
    
    * `Domain RegistrationHandler.ServerCredential` and `DomainRegistrationHandler.ServerCredential.password` or `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias` 
    
    * `DomainRegistrationHandler.DomainServerUrl`

1. Add the following properties to [!DNL flashaccess-refimpl.properties] to support remote key delivery to iOS clients:

    * `HandlerConfiguration.KeyServerCertificate` or `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
