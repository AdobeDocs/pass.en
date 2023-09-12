---
description: You can allow list your iOS apps by using Adobe's machotools tool.
title: Allow list your iOS application
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
---
# Allow list your iOS application {#allowlist-your-ios-application}

You can allow list your iOS apps by using Adobe's machotools tool.

Generally, when you complete a TVSDK application, you can use Adobe Primetime DRM command-line tools to allow list your app.

>[!TIP]
>
>You can also use these tools to create DRM policies and encrypt content.

Allow listing your app ensures that protected content can only be played in your video player. However, allow listing an iOS application requires you to complete special procedure that works with Apple's application submission policies.

Before submitting an iOS app, you need to sign it and publish it to Apple.

>[!NOTE]
>
>Apple strips your developer's signature and re-signs the application with their own certificate.

Because of the re-signing, the allow listing information that you generated before you submitted to the Apple App Store is not useable.

To work with this submission policy, Adobe has created a `machotools` tool that will fingerprint your iOS application to create a digest value, sign this value, and inject this value in your iOS application. After you fingerprint your iOS app, you can submit the app to the Apple App Store. When a user runs your app from the App Store, Primetime DRM does a runtime calculation of the application fingerprint and confirms it with the digest value that was previously injected in the application. If the fingerprint matches, the app is confirmed as being allow listed, and protected content is allowed to play.

The Adobe `machotools` tool is included in the iOS TVSDK SDK, in the [!DNL [...]/tools/DRM] folder.

To use `machotools`: 

1. Generate a key pair.

   To use a utility such as OpenSSL, open a command window and enter the following:

   ```shell
   
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. When prompted, enter a password to protect the private key.

   Passwords should contain at least 12 characters, and the characters should include a mixture of uppercase and lowercase ASCII characters and numbers.
1. To use OpenSSL to generate a strong password for you, open a command window and enter the following:

   ```shell
   
   openssl rand -base64 8
   ```

1. Generate a Certificate Signing Request (CSR).

   To use OpenSSL to generate a CSR, open a Command Window and enter the following: 

   ```shell
   
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Self-sign the cert and enter any duration.

   The following example gives a 20-year expiration: 

   ```shell
   
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Convert the self-signed certificate to a PKCS#12 file:

   ```shell
   
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   You can use the self-signed cert to sign your iOS App. 

1. Update the location of the PFX file and password.
1. Before building your application in Xcode, go to  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** and add the following command to your run script:

   ```shell

   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Execute [!DNL machotools] to generate your app Publisher ID hash value.

   ```shell

   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Create a new DRM Policy or update your existing policy to include the returned Publisher ID hash value.
1. Using the [!DNL AdobePolicyManager.jar], create a new DRM Policy (update your existing policy) to include the returned Publisher ID hash value, an optional App ID, and min and max version attributes in the included [!DNL flashaccess-tools.properties] file.

   ```shell

   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Package the content by using the new DRM policy and confirm the playback of the allow listed content in your iOS app.
