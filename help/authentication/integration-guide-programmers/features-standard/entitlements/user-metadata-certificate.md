---
title: User Metadata Certificate for encryption
description: User Metadata Certificate for encryption
exl-id: 6f5d9a31-945e-418b-a9df-985bdbf29dff
---
# User Metadata Certificate for encryption

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

For encrypted user metadata Adobe Pass Authentication integration you need to have a private/public key-pair.

This document describes a process for generating public key certifcates for use in Adobe Pass Authentication. The process described here makes use of the OpenSSL toolkit.

## Certificate Generation Process Walkthrough (#generation)

1. Download and install the OpenSSL toolkit (http://www.openssl.org).

1. Generate a Certificate Signing Request (CSR):

   * Generate a key pair.  Open a Command / terminal window and run the following command:

     ```bash
     openssl genrsa -des3 -out mycompany-license.key 2048
     ```

   * Generate the CSR. On your command line, run the following:

     ```bash
     openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch
     ```

      You will be prompted to enter the password for the private key.

   * Create a back-up copy of your private key and password. Sample CSR:

      ```
      -----BEGIN CERTIFICATE REQUEST-----
      MIIBnTCCAQYCAQAwXTELMAkGA1UEBhMCU0cxETAPBgNVBAoTCE0yQ3J5cHRvMRIw
      EAYDVQQDEwlsb2NhbGhvc3QxJzAlBgkqhkiG9w0BCQEWGGFkbWluQHNlcnZlci5l
      eGFtcGxlLmRvbTCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEAr1nYY1Qrll1r
      uB/FqlCRrr5nvupdIN+3wF7q915tvEQoc74bnu6b8IbbGRMhzdzmvQ4SzFfVEAuM
      MuTHeybPq5th7YDrTNizKKxOBnqE2KYuX9X22A1Kh49soJJFg6kPb9MUgiZBiMlv
      tb7K3CHfgw5WagWnLl8Lb+ccvKZZl+8CAwEAAaAAMA0GCSqGSIb3DQEBBAUAA4GB
      AHpoRp5YS55CZpy+wdigQEwjL/wSluvo+WjtpvP0YoBMJu4VMKeZi405R7o8oEwi
      PdlrrliKNknFmHKIaCKTLRcU59ScA6ADEIWUzqmUzP5Cs6jrSRo3NKfg1bd09D1K
      9rsQkRc9Urv9mRBIsredGnYECNeRaK5R1yzpOowninXC
      -----END CERTIFICATE REQUEST-----
      ```

1. Send the CSR to a Certificate Authority (CA) (for example, Verisign).

1. The CA will send you the certificate in .p7b format (PKCS#7, Cryptographic Message Syntax Standard)

1. Deploy the .p7b certificate. Convert the PKCS#7 (.p7b) file to a PKCS#12 (PFX file, Personal Information Exchange Syntax Standard) using your private key, and generate the PEM file (concatenated certificate container file):

   * Convert PKCS#7 file to a temporary PEM file. On your command line, run the following:

      ```
      openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem -outform PEM -print_certs
      ```

   * Convert the temporary PEM file to a PFX file.  On your command line, run the following:

      ```
      openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password
      ```

   * Convert the temporary PEM file to a final PEM file. On your command line, run the following:

      ```
      openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM
      ```

1. Send the final PEM file to Adobe to have it configured.

   * The person who ultimately needs to receive the PEM file is the Adobe enablement engineer assigned to your integration / validation. If you aren't working directly with that person, you can find out who to send the file to from your Adobe representative.
   * Adobe supports both a primary and a backup certificate. If your primary certificate becomes compromised in any way, you can revoke it, and switch to the secondary certificate to sign the requestor ID in your app. This will assure a smooth transition between certificates in production, with minimal customer impact.
   * Once Adobe receives the PEM file, authentication engineers will add it to your configuration on the server-side, and confirm receipt of the file.
