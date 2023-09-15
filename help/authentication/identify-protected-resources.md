---
title: Identifying Protected Resources
description: Identifying Protected Resources
exl-id: e96aea02-54b2-491d-ba91-253c0d0e681c
---
# Identifying Protected Resources {#identifying-protected-resources}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

Each authorization request (or request to check authorization) must contain a unique identifier for the protected resource for which the user is requesting access. A protected resource can be any level of authorized content, as agreed between an MVPD and participating Programmers. Potential protected resources must fit into this tree structure of increasingly specific granularity:

- Network
    - Channel
        - Show
            - Episode
                - Asset  
                     
</br>

## Media RSS Format {#media_rss}

Resources can be identified by a simple string (a unique identifier for a channel), or can be represented in Media RSS format (MRSS), as agreed between Adobe (or an Adobe Pass authentication authorized partner) and the participating MVPDs and Programmers. The RSS string used as a resource specifier can include additional information, such as ratings and parental-control metadata.  
 

If you use a simple resource identifier, such as "TNT", it is assumed to represent a channel, and is translated into this RSS resource specifier:

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

A more complex specifier might include, for example, additional rating information. You can pass the entire RSS string to Access Enabler functions that require a resource ID, such as [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

Resource specifiers are opaque to Adobe Pass authentication; they are simply passed through to the MVPD. If the MVPD does not recognize or cannot parse your resource specifier, it returns an error to Adobe Pass authentication, which passes the error back to your `tokenRequestFailed()` callback.

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->
