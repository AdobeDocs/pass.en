---
title: JSON object for entitlement resource ID
description: The following code block provides an example of a JSON object when the entitlement resource ID is a simple text string.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
---
# JSON object for entitlement resource ID {#json-object-for-entitlement-resource-id}

The following code block provides an example of a JSON object when the entitlement resource ID is a simple text string. In this case, the resource ID is the string "resource".

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

The following code block provides an example of a JSON object when the entitlement resource ID is an HTML-encoded mRSS string.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

The following mRSS string is used as the resource id.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 

```
