---
title: Determining if Reference Implementation License Server runs properly
description: Determining if Reference Implementation License Server runs properly
copied-description: yes
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
---
# Determining if Reference Implementation License Server runs properly {#determining-if-reference-implementation-license-server-runs-properly}

There are several ways to determine whether your Reference Implementation License Server has started correctly. You can view the [!DNL catalina.log] logs may not be sufficient, as the license server logs to its own log files. Follow the steps below to ensure your Reference Implementation has started up properly.

* Check your [!DNL AdobeFlashAccess.log] file. This is where the Reference Implementation writes log information. The location of this log file is indicated by your [!DNL log4j.xml] file and can be modified to point to any location you'd like. By default, the log file copied to the working directory where you run catalina. 

* Go to the following URL: [!DNL https:// flashaccess/license/v4]*your server:server port*. You should see the text "License Server is setup correctly".

Another way to test if your server runs correctly is to package a segment of the test content, set up a sample video player, and then play it.

The following procedure describes this process:

1. Go to the [!DNL \Reference Implementation\Command Line Tools] folder.

   See [Installing the command line tools](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) on how to install the command line tools. 

1. Type the following command to create a simple anonymous DRM policy: 

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   See [Command line usage](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) on how to create DRM policies with the DRM Policy Manager. 

1. Set the `encrypt.license.serverurl` property in the [!DNL flashaccesstools.properties] file to the URL of the license server.

   For example, [!DNL https:// localhost:8080/]. The [!DNL flashaccesstools.properties] file is located in the [!DNL \Reference Implementation\Command Line Tools] folder. 

1. Type the following command to package a segment of the content: 

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. Copy the two generated files to the [!DNL webapps\ROOT\Content] folder on the Tomcat server. 
1. Go to the [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] directory and copy the contents to the [!DNL webapps\ROOT\SVP\] folder on the Tomcat server. 

1. Install Flash Player version 10.1 or later. 
1. Open a web browser and go to the following URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Go to the following URL and then click **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*. 

1. If the video fails to play, check if any error codes are displayed in the logging pane of the Sample Video Player or added to the [!DNL AdobeFlashAccess.log] file.

   You can now search for the location of the [!DNL AdobeFlashAccess.log] log file in the log4j.xml file and then modify it. By default, the log file is copied into the working directory where you run catalina.
