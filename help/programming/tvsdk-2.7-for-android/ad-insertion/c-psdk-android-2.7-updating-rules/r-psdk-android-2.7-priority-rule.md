---
description: The priority rule defines the priority order of the ad creatives that will be selected for playback from a VAST/VMAP response.
keywords: priority rule;creative selection rules
title: Priority rules
exl-id: e2aa0bd7-4071-4b42-88aa-73e5172e4f02
---
# Priority rules {#priority-rules}

The priority rule defines the priority order of the ad creatives that will be selected for playback from a VAST/VMAP response.

## A Priority rule has the following attributes and possible values:

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Key</th> 
   <th class="entry"> Type</th> 
   <th class="entry"> Values</th> 
   <th class="entry"> Description</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> priority</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> An array of lowercase mime-types that define the priority in which source creatives must be selected for playback.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Currently only <span class="codeph"> host</span> is supported. This attribute must be present when <span class="codeph"> matches</span> and <span class="codeph"> values</span> attributes are defined.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> multiple</span></td> 
   <td>Possible values:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - equals</li> 
     <li><span class="codeph"> ne</span> - not equals</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> - not contains</li> 
     <li><span class="codeph"> sw</span> - starts with</li> 
     <li><span class="codeph"> ew</span> - ends with</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> priority</span></td> 
   <td>The value must always be <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK will use the <span class="codeph"> matches</span> attribute on the <span class="codeph"> item</span> of the source creative and match against the values defined in this array</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td></td> 
   <td> <p>Value can be <span class="codeph"> vod</span> or <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}

```
