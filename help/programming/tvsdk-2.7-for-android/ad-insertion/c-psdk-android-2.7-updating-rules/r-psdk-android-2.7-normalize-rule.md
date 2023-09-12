---
description: The normalize rule defines a URL transformation to apply to a source creative URL obtained from a VAST/VMAP response.
keywords: normalize rule;creative selection rules
title: Normalize rules
exl-id: 28f315fe-b665-4abb-9b28-0182e999a8b2
---
# Normalize rules {#normalize-rules}

The normalize rule defines a URL transformation to apply to a source creative URL obtained from a VAST/VMAP response.

## The normalize rule has the following attributes and possible values:

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> normalize</span></td> 
   <td>The value must always be <span class="codeph"> normalize</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> String</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Currently only <span class="codeph"> host</span> is supported. This attribute must be present when <span class="codeph"> matches</span> and <span class="codeph"> values</span> attributes are defined.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK will use the <span class="codeph"> matches</span> attribute on the <span class="codeph"> item</span> of the source creative and match against the values defined in this array.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> A regular expression to apply on the source creative URL to match.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> A regular expression to apply on the source creative URL to replace based on the match.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```
