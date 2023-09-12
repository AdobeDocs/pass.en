---
title: Packager Preferences
description: Packager Preferences
copied-description: yes
exl-id: 43e49372-a875-413a-ba27-25e3ce5c64c4
---
# Packager Preferences {#packager-preferences}

This tab contains settings required for packaging content. The following table describes these preferences: 

| Preference | Description |
|--- |--- |
|License Server Transport Certificate|The server transport certificate, issued by Adobe. This certificate is used to secure communications between the client and license server. The file must be located in the Resource Directory.|
|Enable HSM|Specifies whether certificates and credentials are stored on an HSM. If so, preferences related to certificates and credentials will be disabled, and the properties on the HSM tab must be specified.|
|Key Encryption Options|Specifies how the Content Encryption Key is encrypted at packaging time|
|License Server Certificate|The License Server Certificate, issued by Adobe. The file must be located in the Resource Directory. The CEK is encrypted with the public key of the license server. Only holders of the license server private key may decrypt the CEK.|
|Packager Credential|The packager credential, issued by Adobe. This file is used to sign the metadata during packaging.|
|File Name|The `PKCS#12` ( .pfx) file containing certificate and private key. The file must be located in the  Resource Directory.|
|File Password|Password for  .pfx file|
|Global Watched Folder Properties|Specifies settings common to all Watched Folders configured on this server.|
|Check Interval in Milliseconds|Specifies how often Watched Folders should check for new content to package. The server iterates through all the configured Watched Folders, then sleeps for this amount of time.|
|Output File Name Suffix|Specifies a file extension to add to output files. For example, if  .out is specified and the input file is  video.flv, the output file would be  video.out.flv.|
|Backup Input Files|Specifies whether a copy of the original content should be saved. If this option is not selected, the original file will be deleted after packaging has been completed successfully.|
|Input Backup Subfolder Name|If the Backup Input Files option is selected, specifies a folder where input files will be saved. This option specifies a folder name relative to the Watched Folder input directory. If the folder does not exist, it will be created during packaging.|
|Overwrite Existing Output Files|Specifies whether the output file may be overwritten if a file already exists with the same name. If this option is not selected and the output file already exists, processing of the input file will be skipped.|
