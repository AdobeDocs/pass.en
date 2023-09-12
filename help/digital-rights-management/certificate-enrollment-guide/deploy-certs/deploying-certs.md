---
title: Deploy certificates
description: Deploy certificates
copied-description: yes
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
---
# Deploy certificates{#deploy-certificates}

To avoid having the PFX password available in clear text on the License Server, the Reference Implementation and Adobe Primetime DRM Server for Protected Streaming require the password to be encrypted when specified in the configuration file. See *Using the Primetime DRM Reference Implementations* or *Using the Primetime DRM Server* for Protected Streaming for instructions on running the scrambling utilities. Each of these includes its own scramble utility, and the encrypted passwords are not interchangeable between these two License Server implementations.

To deploy the certificates and scrambled password to your license server, see *Using the Primetime DRM Reference Implementations* or *Using the Primetime DRM Server for Protected Streaming*.
