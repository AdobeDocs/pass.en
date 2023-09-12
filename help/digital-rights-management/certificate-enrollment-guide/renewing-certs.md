---
title: Renew certificates
description: Renew certificates
copied-description: yes
exl-id: db130ca5-4e26-447f-b2f4-4eee0838fd56
---
# Renew certificates{#renew-certificates}

You should be aware of the following certificate renewal restrictions that are based on your Adobe Primetime DRM SDK configuration:

* Primetime DRM Production SDK

  Adobe provides the initial set of free certificates for the Primetime DRM Production SDK when you purchase a support contract. If you do not have a support contract, you can purchase a set of renewal certificates that are valid for two years. 
* Primetime DRM Evaluation SDK

  The certificate set for this SDK is valid for one year and cannot be renewed. 
* Primetime DRM Trial SDK

  The Primetime DRM Trial SDK is valid for three months, and Adobe provides one set of free renewal certificates.

## Implementing new certificates and using old certificates for existing content {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

In Primetime DRM, you can allow a license server to issue a license for content that is packaged with previous (or even expired) packager certificates. To configure your server to accept license requests from previously packaged content, provide your old certificate to your server and update your server's configuration file so that the server knows where to find the old certificates. For more information, see *Handling certificate updates when Adobe-issued certificates expire* in *Using the Adobe Primetime DRM SDK for Protecting Content*.

If your server application is based on the Primetime DRM Reference Implementation, you do not have to update your server-side program. In the `flashaccess-refimpl.properties` file, there are fields in which you can specify additional Transport and License Server certificates. If you only have one certificate, you do not have to populate those properties. If you have expired certificates, and want to use these certificates when you issue license responses, you must provide these certificates to the configuration file and restart your server.

To specify old certificates, use the following properties:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx` 
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]` 
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx` 
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
