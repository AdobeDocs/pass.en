---
title: Overview
description: Overview
copied-description: yes
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
---
# AIR Publisher ID utility {#air-publisher-id-utility}

When you build an AIR file, the AIR Developer Tool (ADT) automatically generates a Publisher ID. The AIR Publisher ID utility ( [!DNL AdobePublisherIDUtility.jar]) computes the Publisher ID for an AIR application.

The Publisher ID is unique to the certificate that you use to build an AIR file. If you reuse the same certificate for multiple AIR applications, all AIR applications have the same Publisher ID. An AIR release that succeeds release 1.5.2 does not add the generated Publisher ID to a file. Therefore, if you plan to use an AIR application allow list, use this tool to determine the Publisher ID. 

>[!NOTE]
>
>The Publisher ID that is used for AIR allow list enforcement is not the same as the Publisher ID that the application publisher specifies in the application's [!DNL application.xml] file.

## AIR Publisher ID utility command-line usage {#air-publisher-id-utility-command-line-usage}

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` specifies a path to the AIR application's [!DNL signatures.xml] file, located in the applications [!DNL META-INF] directory 

* `signingcert` specifies the certificate that is used to sign an AIR application

>[!NOTE]
>
>To determine the publisher ID for an Android application, you need to use the `-s` option to specify the certificate used to sign the Android application package (APK). Primetime DRM is required to build Android applications that can play Primetime DRM-protected content.
