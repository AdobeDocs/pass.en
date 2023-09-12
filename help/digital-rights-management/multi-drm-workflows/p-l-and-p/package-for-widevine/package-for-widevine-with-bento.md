---
description: We use both the Bento4 packager and the Adobe offline packager to author encrypted DASH content. Bento4 takes as input unencrypted mp4 content.
title: Package your content with Bento4
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
---
# Packaging content for Widevine and PlayReady {#package-for-widevine}

We use both the Bento4 packager and the Adobe offline packager to author encrypted DASH content. Bento4 takes as input unencrypted mp4 content.

## Package your content with Bento4{#package-your-content-with-bento}

The Bento4 packager expects the input mp4 to be pre-fragmented. The Bento4 packager distribution includes a tool for this. 

**Calling Bento4**

Typical Bento4 packager invocations would look like the examples below: 

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

The example below combines PlayReady and Widevine schemes. In this particular case the packager is adding both Widevine content protection and PlayReady content protection initialization data to the output DASH content. 

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

where

The value for the `--encryption-key` flag is in the form `<base16 encoded key id>:<base16 encoded encryption key>`. 

The `--widevine-header=provider:intertrust#content_id:2a` flag tells the packager to include the pssh box in the manifest, which TVSDK currently requires for playback.

The value for `-playready-header` is for PlayReady license acqusition.

## Package your content with Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager takes as input unencrypted mp4 content.

**Calling Adobe Offline Packager**

A typical adobe offline packager invocation would look like the call below: 

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

In this particular case the offline packager is adding both Widevine content protection and PlayReady content protection initialization data to the output DASH content. The value of `-key_file_path` is for a base64-encoded key. The value of `-playready_LA_URL` is for PlayReady license acqusition.

The conf_path argument points to configuration file that would contain the following:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Because certain Android devices — primarily Amazon Fire TV — do not support audio decryption, audio encryption is optional.
