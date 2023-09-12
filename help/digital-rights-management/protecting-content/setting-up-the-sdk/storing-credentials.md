---
title: Storing credentials
description: Storing credentials
copied-description: yes
exl-id: ceb1bc19-56a0-47ce-affd-ce4ecb896c3b
---
# Storing credentials{#storing-credentials}

The Primetime DRM SDK supports different ways to store credentials, including using a Hardware Security Module (HSM), or as a PKCS12 file. The SDK uses a credential (public key certificate and associated private key) when the private key is required. For example, the packager uses a credential to sign metadata; the License Server uses a credential to decrypt data that has been encrypted with the License Server or Transport public key.

You must closely guard private keys to ensure the security of your content and License Server. PKCS12 is a standard archive file format for storing credentials that have been encrypted with a password. (You can also encrypt and sign the PKCS12 file itself.) The file extension [!DNL .pfx] is commonly used for files that support this format. 

>[!NOTE]
>
>Adobe recommends that you use an HSM for maximum security. 
>
>See the *Adobe Primetime DRM Secure Deployment Guidelines* guide.

>[!NOTE]
>
>As of Java 1.7, 64-bit Sun Java for Windows no longer supports the PKCS11 interfaces that Primetime DRM requires for communicatation with HSM devices. If you plan to use an HSM, you need to use a 32-bit version of Java, or use a JDK that supports the full PKCS11 interfaces.

You can keep a private key on an HSM, and use the Primetime DRM SDK to pass in the credential you obtain from the HSM. If you want to use a credential that is stored on an HSM, you need to use a JCE provider that can communicate with an HSM to get a handle to the private key. Then you need to pass the private key handle, provider name, and certificate that includes the public key to `ServerCredentialFactory.getServerCredential()`.

The SunPKCS11 provider represents one example of a JCE provider that you can use to access a private key on an HSM. Some HSMs are also included with a Java SDK that is bundled with a JCE provider.

See the Sun Java documentation for instructions on how to use this provider.

PEM and DER are ways of encoding a public key certificate. PEM is a base-64 encoding and DER is a binary encoding. Certificate files typically use the extension [!DNL .cer], [!DNL .pem], or [!DNL .der]. Certificates are used where only a public key is required. If a component requires only the public key to operate, it is recommended that you provide that component with the certificate instead of a credential or PKCS12 file.
