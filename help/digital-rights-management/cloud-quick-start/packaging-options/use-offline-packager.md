---
title: Use the included Primetime Offline Packager
description: Use the included Primetime Offline Packager
copied-description: yes
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
---
# Use the included Primetime Offline Packager{#use-the-included-primetime-offline-packager}

Your Primetime Java Packager comes pre-configured with most of the settings you need to package content. There are only a few areas to update in order to get started.

## Update packager properties {#section_99904D35E99944A28FF43D924E516CC2}

Context for the current task

* Update the following packager properties prior to using the configuration file to package your content:

### User-Supplied XML Configuration File Properties

|  Property Name  | Description  |
|---|---|
|  `policy_file`  |  policy file path. Adobe shall provide several pre-configured policies to choose from.  |
|  `pkgr_pfx`  | Packager credentials path. You must supply your own Adobe-issued packager credential ( [!DNL .pfx]) here.  |
|  `pkgr_pfx_pwd`  | Packager credentials password. You must supply the password to your Adobe-issued packager credential here.  |

## Package using command line {#section_DFBE462679E34D62963BE201FD3321F9}

Before packaging content, make sure you've had all required information provided in the configuration file.

* To package content with your configuration file, use the following syntax on the command line:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Sample configuration files to package your content to HLS or HDS format are provided, named [!DNL config_hds.xml] and [!DNL config.hls.xml].

The HDS or HLS content will be output to the [!DNL /output] folder under the Protection Kit directory. All artifacts written to this directory must be hosted on an HTTP web server in order to be played.
