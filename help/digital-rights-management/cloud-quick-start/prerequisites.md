---
title: Prerequisites
description: Prerequisites
copied-description: yes
exl-id: 1b66f7fd-ea2f-4217-b327-910e90ab889d
---
# Prerequisites {#prerequisites}

Before packaging content, a Primetime DRM Packager certificate is required. It must be requested via the Primetime DRM Certificate Enrollment Process. Only a packager certificate is required (no License Server or Transport). Please indicate in the Certificate Request email that the request is for a certificate to use with the DRM Service.

[Certificate Enrollment Guide](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

There are two levels of packaging certificates - PRODUCTION and TRIAL. Content that is packaged using TRIAL certificates is for development use only and will not play after the certificate expires. All licenses issued to TRIAL content will have a maximum hard-coded policy expiration date equal to that of the expiration date of the certificate (if not set in the DRM policy).
