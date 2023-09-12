---
title: Package media
description: Package media
copied-description: yes
exl-id: fc2d1f12-8fab-4e62-8d4c-527911be347f
---
# Package media {#package-media}

Use the Package Media tab to package content. The Packager Properties section displays the Packager settings that were entered in the Preferences tab. To modify these settings, go to the Preferences tab, change the settings, and Save.

If you want to package a single FLV or F4V file, choose the **[!UICONTROL Select Single File]** option and enter the full path to the source file and full path where the encrypted file should be saved.

If you want to package all files in a folder, choose the **[!UICONTROL Select Single Folder]** option. Specify the folder containing the source files. Only files in the Input Folder matching the **[!UICONTROL Input Media File Selection]** criteria will be packaged (files in subfolders are not packaged). Choose to encrypt [!DNL .flv] files, [!DNL .f4v] files, or enter a custom regular expression (for example ".&#42;" encrypts all files in the folder). The encrypted files will be saved in the specified output folder, using the same filename as the original file.

>[!NOTE]
>
>File paths must refer to files available to the packaging server. If you are running the Flash Access Manager on a different machine than the packaging server, you must specify a path that is accessible by the server (either located on a network drive or on the server itself).

The following table describes the Package Media preferences: 

|  Preference  | Description  |
|---|---|
|  Policy File Name(s)  | Select one or more policies from the drop-down list to apply to the content. To select multiple policies, hold down the CTRL key while selecting policies.  |
|  Seconds Unencrypted  | Specifies the number of seconds of content to leave unencrypted at the beginning of the file. To encrypt starting from the beginning, enter "0".  |
|  Encrypt Video  | Select this checkbox to encrypt video data  |
|  Encryption Level  | If video encryption is enabled, select the encryption level for video data. High encrypts all video data. Medium and Low selectively encrypt portions of the video. (Only for F4V with H.264 video)  |
|  Encrypt Audio  | Select this checkbox to encrypt audio data  |
|  Encrypt Script  | Select this checkbox to encrypt script data (FLV only)  |
|  Custom Properties  | Specify custom properties to include in the packaged content. These properties will be available to the license server when issuing a license. (Optional)  |

After the packaging options are selected, click the **[!UICONTROL Package Media]** button to begin packaging the files.
