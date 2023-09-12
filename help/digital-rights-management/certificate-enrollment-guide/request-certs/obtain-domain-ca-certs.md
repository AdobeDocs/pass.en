---
title: Obtain Domain CA certificates
description: Obtain Domain CA certificates
copied-description: yes
exl-id: cad233e0-41f7-4897-ab5f-d5a098c37306
---
# Obtain Domain CA certificates{#obtain-domain-ca-certificates}

Unlike the License Server, Packager or Transport certificate, the Domain CA certificate is not issued by Adobe. You can obtain this certificate from a Certificate Authority, or you can generate a self-signed certificate to use for this purpose.

The Domain CA certificate should use a 1024-bit key and contain the standard attributes required in a CA certificate:

* Basic Constraints extension with the CA flag set to true 
* Key Usage extension specifying Certificate Signing is allowed

For example, using OpenSSL, a self-signed CA certificate can be generated as follows: 

1. Create a file called [!DNL ca-extensions.txt] containing:

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. Generate key:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. Generate CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. Generate certificate:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. Generate password:

   ```
   openssl rand -base64 8 
   ```

1. Generate PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
