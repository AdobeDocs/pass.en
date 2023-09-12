---
title: Handling certificate updates when your Adobe-issued certifcates expire
description: Handling certificate updates when your Adobe-issued certifcates expire
copied-description: yes
exl-id: 9768544e-7e92-4c3a-9863-af9aed74a0c0
---
# Handling certificate updates when your Adobe-issued certifcates expire {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

There might be times when you have to get a new certificate from Adobe. For example, when a production certificate expires, an evaluation certificate expires, or when you switch from an evaluation to a production certificate. When a certificate expires and you do not want to repackage the content that used the old certificate. You can make the License Server aware of both the old and new certificates.

Use the following procedure to update your server with the new certificates:

1. (Optional) When adding new entries to an existing policy update list or revocation list, be sure to sign with the new credentials, and use the old certificate to validate the signature on the existing file.

   For example, use the following command line to add an entry to an existing policy update list, which was signed using a different credential:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Use the Java API to update the license server with the new policy update list or revocation list:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   or:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   In the reference implementation, the properties you use are `HandlerConfiguration.RevocationList` and `HandlerConfiguration.PolicyUpdateList`. Also update the certificate used to verify the signatures: `RevocationList.verifySignature.X509Certificate`. 

1. To consume content that was packaged using the old certificates, the license server requires the old and new license server credentials and transport credentials. Update the license server with the new and old certificates.

   For the license server credentials:

    * Ensure that the current credential is passed into the `LicenseHandler` constructor:

        * In the reference implementation, set it through the `LicenseHandler.ServerCredential` property. 
        * In the Adobe Access Server for Protected Streaming, the current credential must be the first credential specified in the `LicenseServerCredential` element in the flashaccess-tenant.xml file.

    * Ensure that the current and old credentials are provided to `AsymmetricKeyRetrieval`

        * In the reference implementation, set it through the `LicenseHandler.ServerCredential` and `AsymmetricKeyRetrieval.ServerCredential. n` properties. 
        * In the Adobe Access Server for Protected Streaming, the old credentials are specified after the first credential in the `LicenseServerCredential` element in the flashaccess-tenant.xml file.

   For the transport credentials:

    * Ensure that the current credential is passed into the `HandlerConfiguration.setServerTransportCredential()` method:

        * In the reference implementation, set it through the `HandlerConfiguration.ServerTransportCredential` property. 
        * In the Adobe Access Server for protected streaming, the current credential must be the first credential specified in the `TransportCredential` element in the flashaccess-tenant.xml file.

    * Ensure that the old credentials are provided to `HandlerConfiguration.setAdditionalServerTransportCredentials`():

        * In the reference implementation, set it through the `HandlerConfiguration.AdditionalServerTransportCredential. n` properties. 
        * In the Adobe Access Server for protected streaming, this is specified after the first credential in the `TransportCredential` element in the flashaccess-tenant.xml file.

1. Update packaging tools to make sure they are packaging content with the current credentials. Ensure that the latest license server certificate, transport certificate, and packager credential are used for packaging. 
1. To update the Key Server's License Server Certificate:

    * Update the credentials in the Adobe Access Key Server tenant configuration file. Include both the old and new Key Server credentials in flashaccess-keyserver-tenant.xml. 
    * Ensure the current certificate is passed into the `HandlerConfiguration.setKeyServerCertificate()` method.

        * In the reference implementation, set it through the `HandlerConfiguration.KeyServerCertificate` property. 
        * In the Adobe Access Server for Protected Streaming, specify the Key Server's certificate in the through the Configuration/Tenant/Certificates/KeyServer element.
