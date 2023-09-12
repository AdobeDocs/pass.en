---
title: SWF Hash Calculator
description: SWF Hash Calculator
copied-description: yes
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
---
# SWF Hash Calculator{#swf-hash-calculator}

The SWF Hash Calculator utility calculated the digest of a SWF application located in a file. To run the hasher, run the command:

```
Hasher.bat filename.swf
```

or the command:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

The utility output the following message:

```
SWF Hash: hash-of-swf
```

This value can be used to specify the SWF digest in [!DNL flashaccess-tenant.xml].
