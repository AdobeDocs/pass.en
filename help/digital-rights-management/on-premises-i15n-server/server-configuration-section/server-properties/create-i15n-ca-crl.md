---
title: Create Individualization CA CRL
description: Create Individualization CA CRL
copied-description: yes
exl-id: 72147209-1337-4aed-9e4e-210c905c55a4
---
# Create Individualization CA CRL{#create-individualization-ca-crl}

This Certificate Revocation List (CRL) distribution point is included within each machine certificate issued by the individualization server. During machine certificate validation on the license server, this CRL will be downloaded from the distribution point listed in the certificate (or read from the cache if already downloaded) and checked to be sure the certificate has not been revoked.

>[!NOTE]
>
>To set the URL for the CRL distribution point, you will need to set the [!DNL AdobeInitial.properties] `cert.machine.crldp` field. This distribution point is *not* checked by Primetime DRM for validity. You must verify that this URL is valid. Errors resulting from an invalid URL will not become apparent until validation errors appear from the license server.

Outlined below are simplified, sample instructions for using OpenSSL to create CRLs that your license server can consume. Adobe recommends that you perform these steps in a secure fashion and environment, once a Production Individualization CA credential has been obtained. 

1. Change the working directory to the [!DNL create_crl] directory included in this distribution.
1. Copy your Individualization CA [!DNL pfx] to the same [!DNL create_crl] directory.

   The subsequent steps assume that the Individualization CA pfx is named [!DNL i15n.pfx]. Adjust as appropriate for your setup.
1. Extract the Individualization CA [!DNL pfx] file's private key.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Convert the private key to [!DNL pksc8] format.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Generate the CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   This example creates a CRL with a default 1 month validity period. Use the `-crldays` and `-crlhours` options to override the default values.

   Generating a CRL uses the [!DNL index] and [!DNL crlnumber] file pointed to in your [!DNL openssl.conf]. By default, the [!DNL demoCA] location in the working directory is used. Sample [!DNL index] and [!DNL crlnumber] files are included in the supplied [!DNL demoCA] directory. 

1. Deploy the CRL file generated in the previous step to a suitable location that is reachable by the license server (for example: individualization server [!DNL ROOT]).
1. Restart the license server, once the CRL is in place.
