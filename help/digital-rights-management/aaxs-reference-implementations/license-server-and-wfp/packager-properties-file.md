---
title: Packager properties file
description: Packager properties file
copied-description: yes
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
---
# Packager properties file {#packager-properties-file}

Use the [!DNL flashaccess-refimpl-packager.properties] file to configure the Watched Folder Packager component of the reference implementation. At a minimum, be sure to set the license server URL, license server certificate, packager credential, and key protection options. This file also contains the location of each watched folder (packager.watchfolder.source. `n`). Any changes made to the values in this property file will take effect the next time the watched folder packager runs (restarting the server is not required). However, if there is a configuration error in the packager, the watched folder packager thread will exit, and the server will need to be restarted to restart the packager thread.
