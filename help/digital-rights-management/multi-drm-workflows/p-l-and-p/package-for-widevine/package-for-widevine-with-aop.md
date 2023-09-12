---
description: Adobe Offline Packager takes as input unencrypted mp4 content.
title: Package your content with Adobe Offline Packager
exl-id: 4433d76a-57c0-41e6-b358-5408b0fe87e7
---
# Package your content with Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager takes as input unencrypted mp4 content.

  **Calling Adobe Offline Packager**

   A typical adobe offline packager invocation would look like the call below: 

      java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
      -out_path "Jaigo_DASH"
      -key_file_path "Jaigo_DASH/_info/key.B64.random"
      -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
      -widevine_provider intertrust
      -playready_LA_URL
      http://pr.test.expressplay.com/playready/RightsManager.asmx
      -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
      -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

   In this particular case the offline packager is adding both Widevine content protection and PlayReady content protection initialization data to the output DASH content. The value of `-key_file_path` is for a base64-encoded key. The value of `-playready_LA_URL` is for PlayReady license acqusition.

   The conf_path argument points to configuration file that would contain the following:

      <config>
      <frag_dur>4</frag_dur>
      <target_dur>6</target_dur>
      <encrypt_audio>false</encrypt_audio>
      </config>

   Because certain Android devices — primarily Amazon Fire TV — do not support audio decryption, audio encryption is optional.
