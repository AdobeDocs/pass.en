---
title: Enable the usage model demo
description: Enable the usage model demo
copied-description: yes
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
---
# Enable the usage model demo{#enable-the-usage-model-demo}

1. Specify the custom property `RI_UsageModelDemo=true` at packaging time.

   If you are packaging content using the Media Packager command line tool, enter: 

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.
