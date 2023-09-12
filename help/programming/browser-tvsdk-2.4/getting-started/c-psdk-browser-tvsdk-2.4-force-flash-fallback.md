---
description: The forceflash flag in the source list forces Flash fallback for a URL. For this URL, you can use Adobe Flash Player to play the content.
title: Forcing the Flash fallback using the media source list
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
---
# Forcing the Flash fallback using the media source list{#forcing-the-flash-fallback-using-the-media-source-list}

The forceflash flag in the source list forces Flash fallback for a URL. For this URL, you can use Adobe Flash Player to play the content.

In the media source list (for example in the `sources.js` file), you can set `forceflash` to `true`. For example: 

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```
