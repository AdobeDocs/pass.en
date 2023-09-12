---
title: Prepare passwords using Ant
description: Prepare passwords using Ant
copied-description: yes
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
---
# Prepare passwords using Ant{#prepare-passwords-using-ant}

Use Ant to encrypt your password: 

1. Navigate to `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Set the `sdkdir` property in [!DNL build-refimpl.xml] to point to the directory that includes the Primetime DRM Java SDK.
1. Run the following command:

   ```
   ant -f build-refimpl.xml
   ```
