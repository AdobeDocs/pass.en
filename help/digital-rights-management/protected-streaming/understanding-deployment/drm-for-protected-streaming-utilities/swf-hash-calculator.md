---
description: The SWF Hash Calculator utility calculates the digest of a SWF application that is located in a file.
title: SWF hash calculator
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
---
# SWF hash calculator{#swf-hash-calculator}

The SWF Hash Calculator utility calculates the digest of a SWF application that is located in a file.

To run the hasher, type:

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

The utility displays the following message:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

You can use this value to specify the SWF digest in [!DNL flashaccess-tenant.xml].
