---
title: Storing credentials
description: Storing credentials
copied-description: yes
exl-id: 42bccf3a-307f-4763-8b02-f983bcc2e131
---
# Storing credentials{#storing-credentials}

The SDK supports multiple ways of storing credentials (a public key certificate and its associated private key) , including on an HSM or as a PKCS12 file. Credentials are used when the private key is required (for example, for the packager to sign the metadata, or for the License Server to decrypt data encrypted with the License Server or Transport public key). Private keys must be closely guarded to ensure the security of your content and License Server. PKCS12 is a standard format for a file containing a credential encrypted using a password. The file extension .pfx is commonly used for files of this format. 

>[!NOTE]
>
>Adobe recommends using an HSM for maximum security. For more information, see The Adobe Access Secure Deployment Guidelines.

>[!NOTE]
>
>As of Java1.7, 64bit Sun Java for Windows does not support the PKCS11 interfaces that Adobe Access DRM requires in order to communicate with HSM devices. If you plan to use an HSM, please use a 32bit version of Java, or use a JDK that supports the full PKCS11 interfaces.

You can keep a private key on a Hardware Security Module (HSM) and use the SDK to pass in the credential you obtain from the HSM. To use a credential stored on an HSM, use a JCE provider that can communicate with an HSM to get a handle to the private key. Then, pass the private key handle, provider name, and certificate containing the public key to `ServerCredentialFactory.getServerCredential()`.

The SunPKCS11 provider is one example of a JCE provider which can be used to access a private key on an HSM (see the Sun Java documentation for instructions on using this provider). Some HSMs also come with a Java SDK which includes a JCE provider.

PEM and DER are two ways of encoding a public key certificate. PEM is a base-64 encoding and DER is a binary encoding. Certificate files typically use the extension .cer, .pem. or .der. Certificates are used in places where only the public key is required. If a component requires only the public key to operate, it is better to provide that component with the certificate instead of a credential or PKCS12 file.
