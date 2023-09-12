---
title: HSM Preferences
description: HSM Preferences
copied-description: yes
exl-id: 323f839b-fbd8-492c-a210-7651e92c7513
---
# HSM Preferences {#hsm-preferences}

Preferences in this tab only need to be specified if the **[!UICONTROL Enable HSM]** checkbox is selected in the Packager tab. The following table describes these preferences: 

|  Preference  | Description  |
|---|---|
|  Sun PKCS#11 Config File Name  | The full path to the Sun PKCS#11 provider's configuration file. See the Java PKCS#11 Reference Guide on Sun's website for details on the contents of this configuration file.  |
|  Partition Password  | The password for the HSM partition specified in the PKCS#11 configuration file.  |
|  License Server Certificate Alias  |Alias for Adobe-issued license server certificate stored on HSM. This certificate is used to encrypt the CEK during packaging. Specify this instead of *License Server Certificate* in the Packager tab.  |
|  License Server Transport Certificate Alias  |Alias for Adobe-issued server transport certificate stored on HSM. This certificate is used to secure communications between the client and license server. Specify this instead of *License Server Transport Certificate* in the Packager tab.  |
|  Packager Credential Alias  |Alias for Adobe-issued packager credential (certificate and private key) stored on HSM. This is used to sign the metadata during packaging. Specify this instead of *Packager Credential* in the Packager tab.  |
|  License Server Credential Alias  |Alias for Adobe-issued license server credential (certificate and private key) stored on HSM. This credential is used to sign Policy Update Lists. Specify this instead of *License Server Credential* in the Policy Update List tab. (This alias will likely be the same as *License Server Certificate Alias*.)  |
