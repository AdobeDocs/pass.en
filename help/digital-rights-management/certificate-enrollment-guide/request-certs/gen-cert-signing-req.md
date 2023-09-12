---
title: Generate a certificate signing request (Requester)
description: Generate a certificate signing request (Requester)
copied-description: yes
exl-id: 4f8dae3d-da56-453d-b3c4-e67fe4f37064
---
# Generate a certificate signing request (Requester) {#generate-a-certificate-signing-request-requester}

1. Generate a key pair. To use a utility such as OpenSSL, open a Command Window and enter the following:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe recommends including certificate type (lic, pkgr, trans, trial, or eval) in the key name. This naming convention makes it easier when you deploy them on your license server. This example uses "mycompany-license.key". For the Evaluation and Trial versions, use "mycompany-eval.key" and "mycompany-trial.key".

1. Enter a password to protect the private key.

   Passwords should contain at least 12 characters. The characters should include a mixture of uppercase and lowercase ASCII characters and numbers. To use OpenSSL to generate a strong password, open a Command Window and enter the following: 

   ```
   openssl rand -base64 8
   ```

1. Generate a Certificate Signing Request (CSR).

   To use OpenSSL to generate a CSR, open a Command Window and enter the following: 

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. You are prompted to enter the password for the private key.
1. Create a back-up copy of your private key and password.

   If you lose the private key or if it is compromised, contact the Adobe Certificate Administrator to revoke your certificate and request a new one.

   >[!NOTE]
   >
   >Adobe recommends using an HSM to protect your private key and password.
