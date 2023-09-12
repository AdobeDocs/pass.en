---
description: If the client requests tracking information in JSON format, the manifest server sends back a file in one of the JSON formats.
title: JSON formats for tracking URLs
---

# JSON formats for tracking URLs {#json-formats-for-tracking-urls}

If the client requests tracking information in JSON format, the manifest server sends back a file in one of the JSON formats.

## JSON format for tracking version 1 {#json_v1}

The JSON file that the manifest server sends if `pttrackingversion=v1` has the following general format:

```
{ 
"start" : <start-time-of-first-sample-of-playback>, 
"end" : <end-time-of-last-sample-of-playback>, 
"adtracking" : [ { 
"time": <time-offset-relative-to-beginning-of-playback>, 
"trackingurls":[{ 
    "adsystem": <ad-system-of-url1>, 
    "url" : <url1> }, { 
    "adsystem": <ad-system-of-url2>, 
    "url" : <url2>}, ...] 
}, ...]}
```

## JSON format for tracking version 2 {#json_v2}

The JSON file that the manifest server sends if `pttrackingversion=v2` has the format of the following example, which comes from a typical JSON block. 

It has been shortened to avoid unnecessary repetition, so that the structure is clearer. An ellipsis (three dots, separated by spaces) indicates omitted information within some URLs and between some code blocks. Unshortened URLs appear on multiple lines, though they appear on a single line in the JSON file.

```
{ 
  "startTime" : 0.0, 
  "endTime" : 362.508, 
  "scte35" : [ { 
     "offset" : 31.03, 
     "programDateTime" : 31.03, 
     "tagName" : "EXT-X-SCTE35", 
     "tagAttributes" : { 
       "CUE" : "/DBIAAAAAAAA/wBwBQb+D24zFgAyAhdDVUVJQAAABH+fCAgAAAAARERERBAAAAIXQ1VFSUAAAAN/nwgIAAAAADMzMzMRAAB4jsoB", 
       "ID" : "1073741828" 
     } 
   }, { 
   "offset" : 111.1, 
   "programDateTime" : 111.1, 
   "tagName" : "EXT-X-SCTE35", 
   "tagAttributes" : { 
     "CUE" : "/DBIAAAAAAAA/wBwBQb+DskaNQAyAhdDVUVJQAAAAn+XCAgAAAAAIiIiIhAAAAIXQ1VFSUAAAAF/nwgIAAAAABERERERAAAnk2tf", 
     "ID" : "1073741826" 
   } ], 
  "pods" : [ { 
    "id" : "0", 
    "startTime" : 0.0, 
    "duration" : 60.0, 
    "ads" : [ { 
      "id" : "308150", 
      "startTime" : 0.0, 
      "duration" : 15.0, 
      "companions" : [ { 
        "id" : "103", 
        "width" : 300, 
        "height" : 250, 
        "resourceType" : "static", 
        "mimeType" : "image/jpeg", 
        "url" : "https://a.newsinc.com/. . ..jpg", 
        "trackingUrls" : [ { 
          "startTime" : 0.0, 
          "adSystems" : "Auditude", 
          "event" : "creativeView", 
          "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; 
                   u=19287a324825cc5aacb7e46183c72324; 
                   uid=ixutzMD0Se6OSWEmWT1ZdQ;cid=1785961691;s=6c7940cd; 
                   t=1429813545;br=1;sq=1; 
                   pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur%3a60%2clot%3a1%2ccpos%3a1; 
                   ax=0%2c0%2c0%2c0;w=2000;a=308150;a1=103/c300x250.jpeg"}, { 
          "startTime" : 0.0, 
          "adSystems" : "Auditude", 
          "event" : "clickThrough", 
          "url" : "https://example.com?ClickThrough"} ] }, { 
        "id" : "102", 
        "width" : 300, 
        "height" : 250, 
        "resourceType" : "iframe", 
        "mimeType" : "text/html", 
        "url" : "https://ad.qa.auditude.com/adserver/s/a1=102;a=308150;w=2000;z=147611; 
                 u=19287a324825cc5aacb7e46183c72324; 
                 uid=ixutzMD0Se6OSWEmWT1ZdQ;cid=1785961691;s=6c7940cd; 
                 t=1429813545;br=1;sq=1; 
                 pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur%3a60%2clot%3a1%2ccpos%3a1; 
                 ax=0%2c0%2c0%2c0/c300x250.html", 
        "trackingUrls" : [ { 
          "startTime" : 0.0, 
          "adSystems" : "Auditude", 
          "event" : "creativeView", 
          "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; 
                   u=19287a324825cc5aacb7e46183c72324; 
                   uid=ixutzMD0Se6OSWEmWT1ZdQ;cid=1785961691;s=6c7940cd; 
                   t=1429813545;br=1;sq=1; 
                   pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur%3a60%2clot%3a1%2ccpos%3a1; 
                   ax=0%2c0%2c0%2c0;w=2000;a=308150;a1=102/c300x250.html" }, { 
          "startTime" : 0.0, 
          "adSystems" : "Auditude", 
          "event" : "clickThrough", 
          "url" : "https://example.com?ClickThrough" } ] } ], 
      "trackingUrls" : [ { 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp& 
                 cid=1785961691&z=147611&a=308150&s=6c7940cd&t=1429813545& 
                 w=2000&uid=ixutzMD0Se6OSWEmWT1ZdQ&u=19287a324825cc5aacb7e46183c72324& 
                 br=1&sq=1&pod=id:1,ctype:l,ptype:p,dur:60,lot:1,cpos:1& 
                 ax=0,0,0,0" }, { 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& 
                  a=308150&a1=105&ref=urn:asset:308150:105&unit=percent&progress=0& 
                  cid=1785961691&z=147611&a=308150&s=6c7940cd&t=1429813545&w=2000& 
                  uid=ixutzMD0Se6OSWEmWT1ZdQ&u=19287a324825cc5aacb7e46183c72324& 
                  br=1&sq=1&pod=id:1,ctype:l,ptype:p,dur:60,lot:1,cpos:1& 
                  ax=0,0,0,0" }, { 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=0" }, { 
 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; . . ." }, { 
 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp& . . ." }, { 
 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/; . . ." }, { 
 
        "startTime" : 0.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." }, { 
 
        "startTime" : 3.75, 
        "adSystems" : "Auditude", 
        "event" : "first", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." }, { 
 
        "startTime" : 3.75, 
        "adSystems" : "Auditude", 
        "event" : "first", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=25" }, { 
 
        "startTime" : 3.75, 
        "adSystems" : "Auditude", 
        "event" : "first", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." }, 
 
      . . . 
 
       { 
        "startTime" : 15.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." 
       }, { 
        "startTime" : 15.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=100" 
       }, { 
        "startTime" : 15.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." } ] },  
 
    . . .  
 
     { 
      "id" : "308128", 
      "startTime" : 213.0, 
      "duration" : 15.0, 
      "companions" : [ ], 
      "trackingUrls" : [ { 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp . . ." }, { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." }, { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=0" , { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; . . ." }, { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp& . . ." }, { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/;uid=mbAXWlBCTsai4x_FbjJycg; 
                 u=4316135f47263eee860b2174fecd3bba;t=1429813545;s=115f9058;z=147612; 
                 cid=2050307395;br=5;pod=id:5,ctype:l,dur:120,lot:6,cpos:3; 
                 sq=5;ax=0,0,0,0;a1=105;a=308133;w=1000/c0x0" }, { 
 
        "startTime" : 213.0, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." 
      },  
 
      . . . 
 
      { 
        "startTime" : 228.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." 
      }, { 
        "startTime" : 228.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=100" 
      }, { 
        "startTime" : 228.0, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . ." 
      } ] },  
 
    . . .  
 
     { 
        "id" : "102", 
        "width" : 300, 
        "height" : 250, 
        "resourceType" : "iframe", 
        "mimeType" : "text/html", 
        "url" : "https://ad.qa.auditude.com/adserver/s/a1=102;a=307893;w=1500;z=147611; 
                  u=894a4267cd8f1e648eb0bdf878ce3f0a;uid=FmuZ2UwpSjmtBjMc7yLtzw; 
                  cid=159311145;s=cd097e73;t=1429813545;br=1;sq=1; 
                  pod=id%3a1%2cctype%3al%2cdur%3a80%2clot%3a1%2ccpos%3a1; 
                  ax=0%2c0%2c0%2c0/c300x250.html", 
        "trackingUrls" : [ { 
          "startTime" : 347.508, 
          "adSystems" : "Auditude", 
          "event" : "creativeView", 
          "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; 
                    u=894a4267cd8f1e648eb0bdf878ce3f0a;uid=FmuZ2UwpSjmtBjMc7yLtzw; 
                    cid=159311145;s=cd097e73;t=1429813545;br=1;sq=1; 
                    pod=id%3a1%2cctype%3al%2cdur%3a80%2clot%3a1%2ccpos%3a1; 
                    ax=0%2c0%2c0%2c0;w=1500;a=307893;a1=102/c300x250.html" 
        }, { 
          "startTime" : 347.508, 
          "adSystems" : "Auditude", 
          "event" : "clickThrough", 
          "url" : "https://www.example.com?clickThrough" 
        } ] 
      } ], 
      "trackingUrls" : [ { 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp&cid=159311145& 
                  z=147611&a=307893&s=cd097e73&t=1429813545&w=1500& 
                  uid=FmuZ2UwpSjmtBjMc7yLtzw& 
                  u=894a4267cd8f1e648eb0bdf878ce3f0a&br=1&sq=1& 
                  pod=id:1,ctype:l,dur:80,lot:1,cpos:1&ax=0,0,0,0" }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS . . ." }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=0" }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/z=147611; 
                  u=894a4267cd8f1e648eb0bdf878ce3f0a;uid=FmuZ2UwpSjmtBjMc7yLtzw; 
                  cid=159311145;s=cd097e73;t=1429813545;br=1;sq=1; 
                  pod=id%3a1%2cctype%3al%2cdur%3a80%2clot%3a1%2ccpos%3a1; 
                  ax=0%2c0%2c0%2c0;w=1500;a=307893;a1=105/c512x272.mp4" }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "impression", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=adimp& . . ." }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "creativeView", 
        "url" : "https://ad.qa.auditude.com/adserver/i/; . . ." }, { 
 
        "startTime" : 347.508, 
        "adSystems" : "Auditude", 
        "event" : "start", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& . . .0" },  
 
      . . . 
 
       { 
        "startTime" : 362.508, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad4.qa.auditude.com/test.txt?set=1&adprogress=100" }, { 
 
        "startTime" : 362.508, 
        "adSystems" : "Auditude", 
        "event" : "complete", 
        "url" : "https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS& 
                  a=307885&a1=105&ref=urn:asset:307885:105&unit=percent&progress=100& 
                  uid=mbAXWlBCTsai4x_FbjJycg&u=4316135f47263eee860b2174fecd3bba& 
                  t=1429813545&s=115f9058&z=147612&cid=2050307395&br=7& 
                  pod=id:7,ctype:l,dur:120,lot:6,cpos:4&sq=6&ax=0,0,0,0" } ] 
    } ], 
    "trackingUrls" : [ { 
      "startTime" : 302.508, 
      "adSystems" : "Auditude", 
      "event" : "start", 
      "url" : "https://ad.qa.auditude.com/adserver/e?type=podprogress&event=start& 
                uid=mbAXWlBCTsai4x_FbjJycg&u=4316135f47263eee860b2174fecd3bba& 
                t=1429813545&s=115f9058&z=147612&cid=2050307395&br=7& 
                pod=id:7,ctype:l,dur:120,lot:6,cpos:4" }, { 
 
      "startTime" : 362.508, 
      "adSystems" : "Auditude", 
      "event" : "complete", 
      "url" : "https://ad.qa.auditude.com/adserver/e?type=podprogress&event=complete& 
                uid=mbAXWlBCTsai4x_FbjJycg&u=4316135f47263eee860b2174fecd3bba& 
                t=1429813545&s=115f9058&z=147612&cid=2050307395&br=7& 
                pod=id:7,ctype:l,dur:120,lot:6,cpos:4" } ] } ] } 

```

>[!NOTE]
>
>The `offset` value of the `scte35` attribute as extracted from `ad breaks` could be negative. This is because the JSON V2 sidecar contains information about the ad breaks that are partially in the current playback window. So, the `scte35` attribute also contains information about such ad breaks.

## JSON format for tracking version 3 {#json_v3}

The JSON file that the manifest server sends if `pttrackingversion=v3` has the following general format:

```
{ 
  "vmap" : { 
    "vmap:VMAP" : { 
      "@version" : "1.0", "@xmlns:vmap" : "https://www.iab.net/vmap-1.0", 
      "@xmlns:xsi" : "https://www.w3.org/2001/XMLSchema-instance", 
      "vmap:AdBreak" : [ { 
        "@breakType" : "linear", 
        "@breakId" : "0", 
        "@timeOffset" : "00:00:00.000", 
        "vmap:AdSource" : { 
          "@allowMultipleAds" : "true", 
          "@followRedirects" : "true", 
          "@id" : "0", 
          "vmap:VASTData" : { 
            "VAST" : { 
              "@xmlns:xsd" : "https://www.w3.org/2001/XMLSchema", 
              "@xmlns:xsi" : "https://www.w3.org/2001/XMLSchema-instance", 
              "@version" : "3.0", 
              "Ad" : [ { 
                "@sequence" : "1", 
                "@id" : "334690", 
                "InLine" : { 
                  "AdSystem" : "Auditude", 
                  "AdTitle" : "lee_pre_266647", 
                  "Impression" : "https://ad.auditude.com/adserver/e?type=adimp& 
                     a=334690&w=200&uid=JLgOz9mEQGKzPds-INqpEQ& 
                     u=cecebae72a919de350b9ac52602623f3& 
                     t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=1& 
                     pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0", 
                  "Creatives" : { 
                    "Creative" : [ { 
                      "@AdId" : "334690", 
                      "Linear" : { 
                        "Duration" : "00:00:15.139", 
                        "TrackingEvents" : { 
                          "Tracking" : [ { 
                            "@event" : "creativeView", 
                            "#text" : "https://ad.auditude.com/adserver/i/; 
                              uid=JLgOz9mEQGKzPds-INqpEQ; 
                              u=cecebae72a919de350b9ac52602623f3;t=1476120919; 
                              s=74dfbb06;z=266647;cid=371477780;br=1; 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1;sq=1; 
                              ax=0,0,0,0;a1=105;a=334690;w=200/c340x192.m3u8" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://ad.auditude.com/adserver/e? 
                              type=AD_PROGRESS&a=334690&a1=105& 
                              ref=urn:asset:334690:105&unit=percent&progress=0& 
                              uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=1& 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://dpm.demdex.net/ibs:dpid=22619& 
                              dpuuid=JLgOz9mEQGKzPds-INqpEQ" 
                          }, { 
                            "@event" : "firstQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334690&a1=105&ref=urn:asset:334690:105&unit=percent& 
                              progress=25&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3&t=1476120919&s=74dfbb06& 
                              z=266647&cid=371477780&br=1& 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "midpoint", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334690&a1=105&ref=urn:asset:334690:105&unit=percent& 
                              progress=50&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3&t=1476120919&s=74dfbb06& 
                              z=266647&cid=371477780&br=1& 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "thirdQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334690&a1=105&ref=urn:asset:334690:105&unit=percent& 
                              progress=75&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3&t=1476120919&s=74dfbb06& 
                              z=266647&cid=371477780&br=1& 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "complete", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334690&a1=105&ref=urn:asset:334690:105&unit=percent& 
                              progress=100&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3&t=1476120919&s=74dfbb06& 
                              z=266647&cid=371477780&br=1& 
                              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0" 
                          } ] } } } ] } } } ] } } }, 
        "vmap:TrackingEvents" : { 
          "vmap:Tracking" : [ { 
            "@event" : "breakStart", 
            "#text" : "https://ad.auditude.com/adserver/e?type=podprogress&event=start& 
              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=1& 
              pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1" 
          }, { 
            "@event" : "breakEnd", 
            "#text" : "https://ad.auditude.com/adserver/e?type=podprogress&event=complete& 
                       uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1" 
          } ] } }, { 
        "@breakType" : "linear", 
        "@breakId" : "2", 
        "@timeOffset" : "00:06:15.139", 
        "vmap:AdSource" : { 
          "@allowMultipleAds" : "true", 
          "@followRedirects" : "true", 
          "@id" : "2", 
          "vmap:VASTData" : { 
            "VAST" : { 
              "@xmlns:xsd" : "https://www.w3.org/2001/XMLSchema", 
              "@xmlns:xsi" : "https://www.w3.org/2001/XMLSchema-instance", 
              "@version" : "3.0", 
              "Ad" : [ { 
                "@sequence" : "1", 
                "@id" : "334693", 
                "InLine" : { 
                  "AdSystem" : "Auditude", 
                  "AdTitle" : "lee_mid3_266647", 
                  "Impression" : "https://ad.auditude.com/adserver/e?type=adimp&a=334693& 
                    w=200&uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                    t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                    pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0", 
                  "Creatives" : { 
                    "Creative" : [ { 
                      "@AdId" : "334693", 
                      "Linear" : { 
                        "Duration" : "00:00:30.000", 
                        "TrackingEvents" : { 
                          "Tracking" : [ { 
                            "@event" : "creativeView", 
                            "#text" : "https://ad.auditude.com/adserver/i/; 
                              uid=JLgOz9mEQGKzPds-INqpEQ;u=cecebae72a919de350b9ac52602623f3; 
                              t=1476120919;s=74dfbb06;z=266647;cid=371477780;br=3; 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=1; 
                              ax=0,0,0,0;a1=105;a=334693;w=200/c384x216.m3u8" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334693&a1=105&ref=urn:asset:334693:105&unit=percent& 
                              progress=0&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3&t=1476120919&s=74dfbb06& 
                              z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://dpm.demdex.net/ibs:dpid=22619& 
                              dpuuid=JLgOz9mEQGKzPds-INqpEQ" 
                          }, { 
                            "@event" : "firstQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334693&a1=105&ref=urn:asset:334693:105&unit=percent& 
                              progress=25&uid=JLgOz9mEQGKzPds-INqpEQ& 
                              u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "midpoint", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334693&a1=105&ref=urn:asset:334693:105&unit=percent&progress=50& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "thirdQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334693&a1=105&ref=urn:asset:334693:105&unit=percent&progress=75& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0" 
                          }, { 
                            "@event" : "complete", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334693&a1=105&ref=urn:asset:334693:105&unit=percent&progress=100& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0" 
                          } ] } } } ] } } }, { 
                "@sequence" : "2", 
                "@id" : "334759", 
                "InLine" : { 
                  "AdSystem" : "Auditude", 
                  "AdTitle" : "lee_mid2_266652", 
                  "Impression" : "https://ad.auditude.com/adserver/e?type=adimp&a=334759&w=200& 
                                  uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                                  t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                                  pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0", 
                  "Creatives" : { 
                    "Creative" : [ { 
                      "@AdId" : "334759", 
                      "Linear" : { 
                        "Duration" : "00:00:15.000", 
                        "TrackingEvents" : { 
                          "Tracking" : [ { 
                            "@event" : "creativeView", 
                            "#text" : "https://ad.auditude.com/adserver/i/; 
                              uid=JLgOz9mEQGKzPds-INqpEQ;u=cecebae72a919de350b9ac52602623f3; 
                              t=1476120919;s=74dfbb06;z=266647;cid=371477780;br=3; 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=2; 
                              ax=0,0,0,0;a1=105;a=334759;w=200/c320x240.m3u8" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334759&a1=105&ref=urn:asset:334759:105&unit=percent&progress=0& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://dpm.demdex.net/ibs:dpid=22619& 
                              dpuuid=JLgOz9mEQGKzPds-INqpEQ" 
                          }, { 
                            "@event" : "firstQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334759&a1=105&ref=urn:asset:334759:105&unit=percent&progress=25& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0" 
                          }, { 
                            "@event" : "midpoint", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334759&a1=105&ref=urn:asset:334759:105&unit=percent&progress=50& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0" 
                          }, { 
                            "@event" : "thirdQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334759&a1=105&ref=urn:asset:334759:105&unit=percent&progress=75& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0" 
                          }, { 
                            "@event" : "complete", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334759&a1=105&ref=urn:asset:334759:105&unit=percent&progress=100& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0" 
                          } ] } } } ] } } }, { 
                "@sequence" : "3", 
                "@id" : "334691", 
                "InLine" : { 
                  "AdSystem" : "Auditude", 
                  "AdTitle" : "lee_mid1_266647", 
                  "Impression" : "https://ad.auditude.com/adserver/e?type=adimp&a=334691&w=200& 
                                  uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                                  t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                                  pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0", 
                  "Creatives" : { 
                    "Creative" : [ { 
                      "@AdId" : "334691", 
                      "Linear" : { 
                        "Duration" : "00:00:15.023", 
                        "TrackingEvents" : { 
                          "Tracking" : [ { 
                            "@event" : "creativeView", 
                            "#text" : "https://ad.auditude.com/adserver/i/; 
                              uid=JLgOz9mEQGKzPds-INqpEQ;u=cecebae72a919de350b9ac52602623f3; 
                              t=1476120919;s=74dfbb06;z=266647;cid=371477780;br=3; 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=3; 
                              ax=0,0,0,0;a1=105;a=334691;w=200/c384x216.m3u8" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334691&a1=105&ref=urn:asset:334691:105&unit=percent&progress=0& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://dpm.demdex.net/ibs:dpid=22619& 
                              dpuuid=JLgOz9mEQGKzPds-INqpEQ" 
                          }, { 
                            "@event" : "firstQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334691&a1=105&ref=urn:asset:334691:105&unit=percent&progress=25& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0" 
                          }, { 
                            "@event" : "midpoint", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334691&a1=105&ref=urn:asset:334691:105&unit=percent&progress=50& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0" 
                          }, { 
                            "@event" : "thirdQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334691&a1=105&ref=urn:asset:334691:105&unit=percent&progress=75& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0" 
                          }, { 
                            "@event" : "complete", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334691&a1=105&ref=urn:asset:334691:105&unit=percent&progress=100& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0" 
                          } ] } } } ] } } }, { 
                "@sequence" : "4", 
                "@id" : "334705", 
                "InLine" : { 
                  "AdSystem" : "Auditude", 
                  "AdTitle" : "lee_mid1_266652", 
                  "Impression" : "https://ad.auditude.com/adserver/e?type=adimp&a=334705&w=200& 
                                  uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                                  t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                                  pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0", 
                  "Creatives" : { 
                    "Creative" : [ { 
                      "@AdId" : "334705", 
                      "Linear" : { 
                        "Duration" : "00:00:30.069", 
                        "TrackingEvents" : { 
                          "Tracking" : [ { 
                            "@event" : "creativeView", 
                            "#text" : "https://ad.auditude.com/adserver/i/; 
                              uid=JLgOz9mEQGKzPds-INqpEQ;u=cecebae72a919de350b9ac52602623f3; 
                              t=1476120919;s=74dfbb06;z=266647;cid=371477780;br=3; 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=4; 
                              ax=0,0,0,0;a1=105;a=334705;w=200/c340x192.m3u8" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334705&a1=105&ref=urn:asset:334705:105&unit=percent&progress=0& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0" 
                          }, { 
                            "@event" : "start", 
                            "#text" : "https://dpm.demdex.net/ibs:dpid=22619& 
                              dpuuid=JLgOz9mEQGKzPds-INqpEQ" 
                          }, { 
                            "@event" : "firstQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334705&a1=105&ref=urn:asset:334705:105&unit=percent&progress=25& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0" 
                          }, { 
                            "@event" : "midpoint", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334705&a1=105&ref=urn:asset:334705:105&unit=percent&progress=50& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0" 
                          }, { 
                            "@event" : "thirdQuartile", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334705&a1=105&ref=urn:asset:334705:105&unit=percent&progress=75& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0" 
                          }, { 
                            "@event" : "complete", 
                            "#text" : "https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                              a=334705&a1=105&ref=urn:asset:334705:105&unit=percent&progress=100& 
                              uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                              t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                              pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0" 
                          } ] } } } ] } } } ] } } }, 
        "vmap:TrackingEvents" : { 
          "vmap:Tracking" : [ { 
            "@event" : "breakStart", 
            "#text" : "https://ad.auditude.com/adserver/e?type=podprogress&event=start& 
                       uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2" 
          }, { 
            "@event" : "breakEnd", 
            "#text" : "https://ad.auditude.com/adserver/e?type=podprogress&event=complete& 
                       uid=JLgOz9mEQGKzPds-INqpEQ&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120919&s=74dfbb06&z=266647&cid=371477780&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2" 
          } ] } } ] } } }
```

