---
title: Deploy certificates overview
description: Deploy certificates overview
copied-description: yes
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
---
# Overview {#deploy-certificates-overview}

To add certificates to the Adobe Primetime DRM properties files, convert the PKCS#7 file to a PFX file using the private key and generate either a PEM file or a DER file.

* When a credential (certificate and private key) is required, the Primetime DRM command line tools and Adobe HTTP Dynamic Streaming packager require a PFX file. The SDK, Reference Implementation, and Primetime DRM Server for Protected Streaming can accept a PFX file and can also use a credential stored on an HSM. 
* When only a certificate is required, most Primetime DRM components can use a PEM file, DER file, or a certificate on an HSM. The Adobe HTTP Dynamic Streaming packager only accepts DER files for certificates.
