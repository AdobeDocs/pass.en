---
title: Watched folder properties
description: Watched folder properties
copied-description: yes
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
---
# Watched folder properties {#watched-folder-properties}

Each watched folder contains a file called [!DNL properties/watchfolder.properties]. This file contains the packaging options for content placed in this folder, including what to encrypt and which policies to apply. Any changes made to the values in the property file take effect the next time the watched folder packager runs (you do not need to restart the server).

If there is a configuration error in the packager properties file, the packager thread stops. To resume the watched folder packager, restart the server. If there is a configuration error in a watched folder properties file, the watched folder is temporarily removed from the list of folders the packager processes. To add the watched folder back to the list, restart the server or modify the packager properties file. If an error occurs during packaging of a particular file (for example, because the file is corrupt), the file is skipped and the remaining files in the folder are processed.
