---
title: Avoid Using '&'reg_code in /authenticate Request
description: Avoid Using '&'reg_code in /authenticate Request
exl-id: c0ecb6f9-2167-498c-8a2d-a692425b31c5
---
# (Legacy) Avoid Using '&'reg_code in /authenticate Request {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>



## Issue

The IE 9 browser interprets '\&reg' as a special command and converts it to &reg;. 

## Explanation

If the `/authenticate` request is composed as follows...

 
```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...it will be interpreted by IE browser like below and will be sent to Adobe in this format:

 
```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

The requestor\_id will be interpreted as univision&reg;\_code=EKAFMFI, since there is no '&', and Adobe will not find a `regCode` param to associate the token with.  There is a chance that the AuthN token will not be created at all, in which case `/checkauthn` calls will fail to find any tokens.



## Solution

One of the following options should solve this issue:

1.  Avoid using the `&reg_code` param between the other query string params.  Instead move it to the first query-string parameter in the request URL, making the request url like this:  
     
    
        <FQDN>authenticate?reg_code =EKAFMFI&requestor_id=someRequestor&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
    
      
    In this way, the `&reg` param will not be interpreted incorrectly.

1.  Normalize `&reg_code` as using `&amp;reg_code`.

1.  Adobe could introduce a new feature to send an error code back to the 2nd screen in response to an authentication call, if the AuthN token creation failed.
