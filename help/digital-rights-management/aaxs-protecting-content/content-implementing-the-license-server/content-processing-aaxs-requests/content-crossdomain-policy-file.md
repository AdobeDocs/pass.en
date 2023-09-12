---
title: Crossdomain policy file
description: Crossdomain policy file
copied-description: yes
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
---
# Crossdomain policy file {#crossdomain-policy-file}

If the license server is hosted on a different domain than the video playback SWF, then a cross-domain policy file (crossdomain.xml) is necessary to allow the SWF to request licenses from the license server. A cross-domain policy file is an XML file that provides a way for the server to indicate that its data and documents are available to SWF files served from other domains. Any SWF file served from a domain specified in the license server's cross-domain policy file is permitted to access data or assets from that license server.

Adobe recommends that developers follow best practices when deploying the cross-domain policy file by only allowing trusted domains to access the license server and limiting the access to the license sub-directory on the web server.

For more information on cross-domain policy files, please see the following locations:

* Web site controls (policy files)
* Cross-domain policy file specification: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
