---
title: Determining if Reference Implementation License Server is running properly
description: Determining if Reference Implementation License Server is running properly
copied-description: yes
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
---
# Determining if Reference Implementation License Server is running properly {#determining-if-reference-implementation-license-server-is-running-properly}

There are several ways to determine whether your server has started correctly. Viewing the [!DNL catalina.log] logs may not be sufficient, as the license server logs to its own log files. Follow the steps below to ensure your Reference Implementation has started up properly.

* Check your [!DNL AdobeFlashAccess.log] file. This is where the Reference Implementation writes log information. The location of this log file is indicated by your [!DNL log4j.xml] file and can be modified to point to any location you'd like. By default, the log file will be output to the working directory where you've run catalina.

* Navigate to the following URL: `https:///flashaccess/license/v4<your server:server port>`. You should see the text "License Server is setup correctly".

Another way to test if your server is running correctly is to package a piece of test content, set up a sample video player, and play it. The following procedure describes this process:

1. Navigate to the [!DNL \Reference Implementation\Command Line Tools] folder. For information on installing the command line tools, see [Installing the command line tools](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Create a simple anonymous policy by using the following command: 

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   For more information on creating policies using the Policy Manager, see [Command line usage](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Set the `encrypt.license.serverurl` property in the [!DNL flashaccesstools.properties] file to the URL of the license server (for example, `https:// localhost:8080/`). The [!DNL flashaccesstools.properties] file is located under the [!DNL \Reference Implementation\Command Line Tools] folder.

1. Package a piece of content by using the following command: 

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. Copy the 2 generated files to the Tomcat [!DNL webapps\ROOT\Content] folder.
1. Navigate to `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` and copy the contents to the Tomcat `webapps\ROOT\SVP\` folder.
1. Install Flash Player 10.1 or later.
1. Open the web browser and navigate to the following URL:

   `https:// localhost:8080/SVP/player.html`
1. Navigate to the following URL, then click the Play button:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. If the video fails to play, check if any error codes were written in the logging pane of the Sample Video Player, or in the `AdobeFlashAccess.log` file. The location of the `AdobeFlashAccess.log` log file is indicated by your log4j.xml file, and can be modified to point to any location you'd like. By default, the log file is written to the working directory where you've run catalina.
