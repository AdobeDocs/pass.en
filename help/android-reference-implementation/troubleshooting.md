---
title: Troubleshooting
description: Troubleshooting
copied-description: yes
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
---
# Troubleshooting{#troubleshooting}

* For some older devices that are running API level 10 or older, logcat is unable to open the log device because of a permissions issue. The following exception appears: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Workaround:**

  1. Open [!DNL AndroidManifest.xml] under the [!DNL CatalogActivity] project in the workspace. 
    
  1. Add the following permission to the [!DNL `AndroidManfest.xml`] file:
    
     ```    
     android.permission.READ_LOGS
     ```
