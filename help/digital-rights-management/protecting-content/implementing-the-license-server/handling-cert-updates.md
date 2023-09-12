---
title: Handling certificate updates when Adobe-issued certificates expire
description: Handling certificate updates when Adobe-issued certificates expire
copied-description: yes
exl-id: 9051a647-87ed-4df6-8bbc-bb5c112383ee
---
# Handling certificate updates when Adobe-issued certificates expire{#handling-certificate-updates-when-adobe-issued-certificates-expire}

You may need to obtain a new certificate from Adobe. For example, a production certificate expires when an evaluation certificate expires or when you switch from an evaluation to a production certificate. Whenever a certificate expires and you do not want to repackage the content that uses the old certificate, you can make the License Server aware of both the old and new certificates.

To update a server with new certificates:

1. (Optional) When you add new entries to an existing DRM policy update list or revocation list, you need to sign with the new credentials and use the old certificate to validate the signature on the existing file.

   For example, you can use the following command line to add an entry to an existing DRM policy update list, which has been signed using a different credential:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Optional) Use the Java API to update the license server with the new DRM policy update list or revocation list: 

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   or:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   In the reference implementation, the properties that you use are `HandlerConfiguration.RevocationList` and `HandlerConfiguration.PolicyUpdateList`. You also need to update the certificate that is used to verify the signatures: `RevocationList.verifySignature.X509Certificate`. 

1. Update the license server with the new and old certificates.

   If you want to consume content that has been packaged using the old certificates, make sure that the license server has access to the old and new license server credentials as well as transport credentials.

   For the license server credentials:

    * Ensure that the current credential is passed to the `LicenseHandler` constructor:

        * In the reference implementation, set it with the `LicenseHandler.ServerCredential` property. 
        * In the Adobe Primetime DRM Server for Protected Streaming, the current credential must be the first credential that are specified in the `LicenseServerCredential` element in the flashaccess-tenant.xml file.

    * Ensure that the current and old credentials are provided to `AsymmetricKeyRetrieval`

        * In the reference implementation, set it with the `LicenseHandler.ServerCredential` and `AsymmetricKeyRetrieval.ServerCredential. n` properties. 
        
        * In the Primetime DRM Server for Protected Streaming, the old credentials are specified after the first credential in the `LicenseServerCredential` element in the flashaccess-tenant.xml file.

   For the transport credentials:

    * Ensure that the current credential is passed to the `HandlerConfiguration.setServerTransportCredential()` method:

        * In the reference implementation, set it with the `HandlerConfiguration.ServerTransportCredential` property. 
        * In the Primetime DRM Server for protected streaming, the current credential must be the first credential specified in the `TransportCredential` element in the [!DNL flashaccess-tenant.xml] file.

    * Ensure that the old credentials are provided to `HandlerConfiguration.setAdditionalServerTransportCredentials`():

        * In the reference implementation, set it with the `HandlerConfiguration.AdditionalServerTransportCredential. n` properties. 
        * In the Primetime DRM Server for protected streaming, this is specified after the first credential in the `TransportCredential` element in the flashaccess-tenant.xml file.

1. Update the packaging tools to make sure that they are packaging content with the current credentials. Ensure that the latest license server certificate, transport certificate, and packager credential are used for packaging. 
1. Update the Key Server's License Server Certificate as follows:

    * Update the credentials in the Adobe Primetime DRM Key Server tenant configuration file by including both the old and new Key Server credentials in flashaccess-keyserver-tenant.xml. 
    * Ensure the current certificate is passed to the `HandlerConfiguration.setKeyServerCertificate()` method.

        * In the reference implementation, set it with the `HandlerConfiguration.KeyServerCertificate` property. 
        * In the Primetime DRM Server for Protected Streaming, specify the Key Server's certificate in the through the Configuration/Tenant/Certificates/KeyServer element.
