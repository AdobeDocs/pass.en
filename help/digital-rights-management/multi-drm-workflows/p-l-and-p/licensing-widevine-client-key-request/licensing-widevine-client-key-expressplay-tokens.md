---
description: You can generate Expressplay tokens for their encrypted content by sending token requests to the appropriate Expressplay token server.
title: Expressplay tokens
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
---
# Expressplay tokens {#expressplay-tokens}

You can generate Expressplay tokens for their encrypted content by sending token requests to the appropriate Expressplay token server.

An example is the following URL: 

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

The content encryption key storage ID or CEKSID given to the `kid` parameter and the content encryption key or CEK given to the `contentKey` parameter must match the content encryption key storage ID and content encryption key used for packaging. The following text is an example of the token server response:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

You can then either

* use the returned URL and query as the license server URL, or 
* take out the query from the URL and pass in the ExpressPlayToken separately as a HTTP POST header
