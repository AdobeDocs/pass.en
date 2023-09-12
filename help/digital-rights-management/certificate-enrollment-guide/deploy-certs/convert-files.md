---
title: Convert files
description: Convert files
copied-description: yes
exl-id: 7344ca2f-5307-403b-a6fc-cbbea7c2829f
---
# Convert files{#convert-files}

Using a utility such as OpenSSL and the private key the Requester generates the PKCS#12 (pfx) and PEM/DER files by entering the following commands from a Command Window: 

1. Convert PKCS#7 file to a temporary PEM file.

   To use OpenSSL, open a Command Window and enter the following:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >This temporary PEM contains your certificate and the certificates for Intermediate CAs. Use these certificates to generate the PFX file.

1. Convert the temporary PEM file to a PFX file.

   To use OpenSSL, open a Command Window and enter the following:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Convert the temporary PEM file to a final PEM file.

   To use OpenSSL, open a Command Window and enter the following:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Although not required, Adobe recommends using different passwords for the private key (private_key_password) and the PFX (pfx_password).

   This final PEM file contains only your certificate. 

1. Convert the PEM file to a DER file.

   To use OpenSSL, open a Command Window and enter the following:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER files are required only for the HTTP Dynamic Streaming packager.
