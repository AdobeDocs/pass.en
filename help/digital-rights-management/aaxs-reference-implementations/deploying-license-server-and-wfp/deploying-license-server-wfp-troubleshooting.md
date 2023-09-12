---
title: Troubleshooting
description: Troubleshooting
copied-description: yes
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
---
# Troubleshooting {#troubleshooting}

Listed below are common problems and solutions for deployment:

* If you see the following error:

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Make sure the password is encrypted using the provided `ScrambleUtil` class. 

* If you see the following error:

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Make sure you specified the correct encrypted password for the PFX file. 

* If you see the following error:

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Make sure you used the password scrambler class provided with the Reference Implementation (this scrambler utility is different from the one provided with the Adobe® Access™ Server for Protected Streaming).
