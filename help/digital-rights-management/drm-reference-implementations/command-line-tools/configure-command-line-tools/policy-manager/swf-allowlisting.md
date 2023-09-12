---
title: SWF application allow listing
description: SWF application allow listing
copied-description: yes
exl-id: ae8b7f52-897f-43f9-ac7b-665d4b8c16b8
---
# SWF application allow listing {#swf-application-allowlisting}

To allow list a SWF application, you can follow one of these two strategies:

* You can specify a URL to a SWF. This is a very flexible approach, especially in a development environment in which you are rebuilding your SWF regularly. 
* You can specify a SWF HASH. This is a cryptographic digest value of your SWF. This approach is less flexible (but much more strict), since the SWF HASH will change when the application changes and is rebuilt. In this situation, all content bound to the previous HASH will fail to play on the new player and will have to be repackaged. The [!DNL PolicyManager.jar] tool will automatically compute the hash if you specify a [!DNL .swf] file.

  On the other hand, if you are using Primetime DRM via Flash/Adobe Media Server (FMS/AMS), you can supply the path to your particular SWF(s), and FMS/AMS will automatically hash the SWFs for you to insert into the DRM policy that is used to package the content streamed by FMS/AMS.

See `policy.allowedSWFApplication.n` in *Configuration properties* for details.
