---
title: Primetime Offline Packager 2.x releases
description: What's new in Primetime Offline Packager 2.1 and 2.3.1 releases
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
---
# Primetime Offline Packager releases {#primetime-offline-packager-x-releases}

What's new in Primetime Offline Packager 2.1 and 2.3.1 releases

## What's new in Primetime Offline Packager 2.3.1 (Oct 2016)  {#what-s-new-in-primetime-offline-packager-oct}

The release enables On-demand Profile for MPEG-DASH, adds support for the `validate` option for PlaylistCreator tool, and has few key fixes for Multi-DRM scenarios listed below.

| **Issue number** |**Description** |
|---|---|
| PTPUB-985 |HLS AAXS and Sample-AES does not work for packager-generated key |
| PTPUB-973 |Fixed error in encryption algorithm for some specific Widevine content |
| PTPUB-964 |CENC encryption broken for certain media types on certain player - Android TVSDK. |
| PTPUB-954 |Sample-AES encryption bypasses AAXS DRM by default / Error thrown with remote key delivery enabled. |
| PTPUB-951 |Offline packager does not throw exception when key_file_path is not specified with Widevine. It throws NPE instead. |

The latest documentation of Primetime Packagers is available at [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Known issue in version 2.3.1 {#known-issue-in-version}

The following issues exist in this release.

| **Issue number** |**Description** |
|---|---|
| PTPUB-1005 |PlaylistCreator does not provide the correct URL for the .pssh file in the final set level .mpd file generated for the AAXS DRM. |
| PTPUB-1001 |PlaylistCreator should throw error when empty path is provided via in_path parameter |
| PTPUB-990 |For DASH, Offline Packager does not write packager generated IV to disk when the parameters `log_vi` & `iv_out_path` are specified. |
| PTPUB-980 |When configuration file is used for packaging, using the parameter `key_url` does not remove the quotation marks from the provided inputs. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Minimum system requirements {#minimum-system-requirements}

Supported operating systems

* Linux CentOS 6.3 64 bit

Hardware requirements

* 3.2GHz Intel® Pentium® 4 processor (dual Intel Xeon® or faster recommended)

* 64-bit operating systems: 4GB of RAM (8GB recommended)

* Hard Disk

(Disk-SAS): Minimum 10GB with 7.5K RPM

(Disk-SSD): 400MBps read/write speed

(NAS): 1 GB dedicated link

Software requirements

* Oracle Java SE 1.8 or higher

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Download the Java SE software from the [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) and follow the install instructions.
1. Extract the Adobe Primetime Offline Packager 2.3.1 archive file named `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` to the disk.

### Configuring the Offline Packager 2.3.1 {#configuring-the-offline-packager}

The configuration instructions are available in the Primetime Offline Packager Getting Started guide at [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## What's new in Primetime Offline Packager 2.1 (July 2015) {#what-s-new-in-primetime-offline-packager-july}

Support for PlayReady BuyDRM (for DASH). For details, refer to Help Documentation [available here](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

Following enhancement was also made to the offline packager.

PTPUB-780 Added support for EXT-X-START tag

## What's new in Primetime Offline Packager 2.0 (June 2015) {#what-s-new-in-primetime-offline-packager-june}

Clear DASH output support has been added. Refer to product documentation [here](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) for details.

Following issues were also fixed in this release.

* PTPUB-783 Offline Packager can now handle empty WebVTT files.
* PTPUB- 781 Artifacts in HLS output on Chrome when certain transcoded MP4 assets are packaged with offline packager to produce MBR output.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Minimum system requirements {#minimum-system-requirements-1}

**Supported operating systems**

* Linux CentOS 6.3 64 bit

**Hardware requirements**

* 3.2GHz Intel® Pentium® 4 processor (dual Intel Xeon® or faster recommended)

* 64-bit operating systems: 4GB of RAM (8GB recommended)

* 1Gb Ethernet card recommended (multiple network cards and 10Gb also supported)

* Hard Disk

  * (Disk-SAS): Minimum 10GB with 7.5K RPM
  * (Disk-SSD): 400MBps read/write speed
  * (NAS): 1 GB dedicated link

**Software requirements**

* Oracle Java SE 1.8 or higher

### Installing Offline Packager 2.1 {#installing-offline-packager}

1. Download the Java SE software from the [Oracle site](https://www.oracle.com/technetwork/java/javase/downloads/index.html) and follow the install instructions. 
1. Extract the `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, to your disk.

### Configuring the Offline Packager 2.1 {#configuring-the-offline-packager-1}

Refer the Primetime Offline Packager Getting Started document for the configuration details available here [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://helpx.adobe.com/support/primetime.html) page.
