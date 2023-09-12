---
title: Build the BEES reference implementation
description: Build the BEES reference implementation
copied-description: yes
exl-id: 330c14de-fe4e-4cc8-b0a5-8f7c74417adf
---
# Build the BEES reference implementation {#build-the-bees-reference-implementation}

 Ensure you are using Java 1.6.0_24 or later. 
1. Fill in the needed empty paths such as `tomcatdir` and `fasterxmldir` in [!DNL build-bees.xml]

   FasterXML/Jackson is included. You can also download it from [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Update actual jar filenames in [!DNL build.common.xml] if you want to use a different version of the Jackson libraries.
1. Run the `all` target of [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

The [!DNL bees.war] will be created in the [!DNL bees-build/wars] folder.
