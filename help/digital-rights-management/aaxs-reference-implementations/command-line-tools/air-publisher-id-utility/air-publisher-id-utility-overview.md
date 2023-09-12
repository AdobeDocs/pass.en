---
title: AIR Publisher ID utility overview
description: AIR Publisher ID utility overview
copied-description: yes
exl-id: ad982ec8-0180-4185-8752-08592cabef3d
---
# AIR Publisher ID utility overview {#air-publisher-id-utility-overview}

As part of the process of building an AIR file, the AIR Developer Tool (ADT) generates a Publisher ID. This is an identifier that is unique to the certificate used to build the AIR file. If you reuse the same certificate for multiple AIR applications, they will have the same Publisher ID.The AIR Publisher ID utility is used to compute the Publisher ID for an AIR application. AIR releases after 1.5.2 do not write the generated Publisher ID to a file, so it is necessary to use this tool to determine the Publisher ID if you are using an AIR application allow list.

>[!NOTE]
>
>The Publisher ID, used for AIR allow list enforcement, is not the same as the Publisher ID specified by the application publisher in the application's [!DNL application.xml] file.
