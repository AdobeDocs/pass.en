---
title: Opportunity Generator
description: Opportunity Generator
copied-description: yes
exl-id: ee8d239f-7c52-44ea-a238-cc46d46cf128
---
# Opportunity Generatorr{#opportunity-generator}

```
if (resource.metadata != null) { 
 // push in the CustomRangeResolver before other resolvers 
    if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_DELETE_RANGES_METADATA_KEY) 
        result.push(new CustomRangeResolver()); 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_REPLACE_RANGES_METADATA_KEY)) 
        result.push(new CustomRangeResolver()); 
    if (resource.metadata.containsKey(DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY)) { 
        result.push(new CustomAdResolver());    // no ad insertion with mark ranges 
    } 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
        if (_auditudeResolver == null) { 
              _auditudeResolver = new AuditudeResolver(); 
        } 
        result.push(_auditudeResolver); 
    } 
    else if (resource.metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY)) { 
        result.push(new MetadataResolver()); 
    } 
}
```
