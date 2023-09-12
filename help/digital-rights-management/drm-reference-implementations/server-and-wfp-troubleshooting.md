---
title: Troubleshooting
description: Troubleshooting
copied-description: yes
exl-id: 6c4f15b6-507e-496e-ad1c-702ce77dd069
---
# Troubleshooting{#troubleshooting}

Following are some problems and solutions you may encounter during deployment.

* If the following error message is displayed: 

  ```
  "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Ensure that the password has been encrypted with the `ScrambleUtil` class. 

* If the following error message is displayed: 

  ```
  "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Make sure that you have specified the correct encrypted password in the PFX file. 

* If the following error message is displayed: 

  ```
  "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Ensure that you use the password scrambler class *that has been provided with the Reference Implementation*. This scrambler utility is different from the one that has been provided with the Adobe Primetime DRM Server for Protected Streaming.
