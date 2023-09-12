---
description: Browser TVSDK currently supports the playback of streams where manifests and fragments do not contain extensions.
title: Extensionless streams
exl-id: ef81bfd2-2bfa-4ff7-b826-fd80802b3c07
---
# Extensionless streams{#extensionless-streams}

Browser TVSDK currently supports the playback of streams where manifests and fragments do not contain extensions.

## Fragment level {#section_0E035129501D4A77BBC14192D8A53A86}

Browser TVSDK parses the first few bytes of the response to detect the content type of extensionless fragments. If no valid content type is detected, Browser TVSDK will throw an error.

## Manifest level {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

Browser TVSDK uses the `mediaResource.resourceType` parameter that is passed in the `replaceCurrentResource` method to detect the content type of manifest URL. For more information, see the `AdobePSDK.MediaPlayer` class.

In the UI Framework player, you can specify the resource type in media resource as follows: 

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 

```

If `resourceType` is not provided, the UI Framework determines the resource type from resource URL extension, which is then passed to `replaceCurrentResource` method. 

>[!TIP]
>
>For extension-less manifest, ensure that `resourceType` is always passed while loading a resource in the UI Framework.
