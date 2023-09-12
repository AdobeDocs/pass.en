---
title: Getting Started
description: Getting Started
copied-description: yes
exl-id: d29d141e-913c-4b9d-979c-91c486414071
---
# Getting Started {#getting-started}

This document provides the steps for a quick setup and deployment of an Adobe Primetime DRM ecosystem that uses Progressive Download to distribute content, and the Primetime DRM Server for Protected Streaming for license distribution. Additional details on each step is provided in the following guides:

* *Using the Primetime DRM Server for Protecting Content* 
* *Using the Primetime DRM Server for Protected Streaming*

The Primetime DRM Server for Protected Streaming is a minimal-functionality server that does not include source code. For a modifiable server with full Java source, see the *Using the Primetime DRM Reference Implementations* guide. If you set up up a Reference License server, that replaces the *Setup and deploy Primetime DRM Server for Protected Streaming (License Server)* step.

## Prerequisites {#prerequisites}

Before you get started, complete the following tasks:

* Get two Windows or Linux computers:

    * One computer will be the License Server. 
    * One computer will be the Content Server.

* Install the following applications on both computers:

    * Tomcat 6.0.18 
    * Java 1.6

## Obtain Certificates {#obtain-certificates}

After the SDK software is delivered, the designated Company Certificate Administrator will receive an invitation to complete the Adobe Primetime DRM Certificate Enrollment registration process. For more information, see the *Primetime DRM Certificate Enrollment Guide*. 

1. The Administrator appoints at least one individual to act as the Certificate Requester.
1. The Certificate Requester generates a private key and a CSR.
1. The Requester submits a certificate request.
1. The Company Administrator approves the request.
1. The Adobe Certificate Administrator confirms the submission.
1. The Requester receives the certificate, binds the certificate with the private key, and deploys the cerfiticate. as described in .

   For more information about deploying the certificate, see the *Deploying the Adobe Primetime DRM Server for Protected Streaming* guide.
1. Steps 3 through 6 must be completed for each certificate type.

   For the Primetime DRM Production version, the Requester must make separate requests for the License Server, Packaging, and Transport certificates, which are valid for two years.

   Customers that use the Primetime DRM Evaluation or Trial versions only need one certificate that is valid for 1 year / 90 days, respectively.
