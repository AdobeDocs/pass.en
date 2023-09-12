---
title: Upgrading existing deployments
description: Upgrading existing deployments
copied-description: yes
exl-id: e07b883f-d5f7-40d3-9221-a0dc2d859a5a
---
# Upgrading existing deployments {#upgrading-existing-deployments}

To upgrade a server running the version 3.0 Reference Implementation License Server or Watched Folder Packager, replace the [!DNL .war] files deployed on your Application Server with the files included with Adobe Access Reference Implementation Server.

If you plan to use domain registration with the Reference Implementation License Server, several new database tables are required. To re-create the entire reference implementation database, run `CreateSampleDB.sql`. To preserve the existing database records and add the new tables, open `CreateSampleDB.sql`and only run the commands to create the following tables:

* `DomainServerInfo` 
* `DomainKeys` 
* `DomainMembership` 
* `UserDomainMembership` 
* `UserDomainRefCount`

The following properties must be added to flashaccess-refimpl.properties to use the domain support:

* `HandlerConfiguration.DomainCAs.n` or `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n` 

* `Domain RegistrationHandler.ServerCredential` and `DomainRegistrationHandler.ServerCredential.password`, or `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias` 

* `DomainRegistrationHandler.DomainServerUrl`

The following properties must be added to [!DNL flashaccess-refimpl.properties] to support remote key delivery to iOS clients:

* `HandlerConfiguration.KeyServerCertificate` or `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
