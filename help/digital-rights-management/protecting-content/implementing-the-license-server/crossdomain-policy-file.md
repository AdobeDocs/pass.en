---
title: Crossdomain DRM policy file
description: Crossdomain DRM policy file
copied-description: yes
---

# Crossdomain DRM policy file {#crossdomain-drm-policy-file}

If the license server is hosted on a different domain than the video playback SWF, then a cross-domain DRM policy file ( [!DNL crossdomain.xml]) is needed to enable the SWF to request licenses from a license server. A cross-domain DRM policy file is represented by an XML file that enables the server to indicate that its data and documents are available to SWF files served from other domains. Any SWF file served from a domain specified in the license server's cross-domain DRM policy file is permitted to access data or assets from that license server.

Adobe recommends that developers follow best practices when deploying the cross-domain policy file by only allowing trusted domains to access the license server and limiting the access to the license sub-directory on the web server.

For more information on cross-domain DRM policy files, see the following locations:

* Web site controls (DRM policy files)
* Cross-domain DRM policy file specification: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

