---
description: The FairPlay license token interface provides production and test services.
title: FairPlay license token request / response
exl-id: 7073a74b-d907-4d45-8550-4305655c33f5
---
# FairPlay license token request and response {#fairplay-license-token-request-response}

The FairPlay license token interface provides production and test services. This request returns a token that can be redeemed for a FairPlay license.

**Method: GET, POST** (with a www-url-encoded body that contains parameters for both methods)

**URLs:**

* **Production:** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Test:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **Sample request:** 

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **Sample Response:**

  ```
  https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
  ```

**Request Query Parameters**

**Table 3: Token Query Parameters**

|Query Parameter|Description|Required?|
|--- |--- |--- |
|customerAuthenticator Customer authenticator as query parameter customerAuthenticator FairPlay|This is your customer API key, one each for your production and test environments. You can find this on the ExpressPlay Admin Dashboard tab.|Yes|
|errorFormat|Either html or json. If html  (the default) an HTML representation of any errors is provided in the entity body of the response. If json is specified, a structured response in JSON format is returned. See [JSON Errors](https://www.expressplay.com/developer/restapi/#json-errors) for details. The mime type of the response is either text/uri-list on success, text/html for HTML error format, or application/json for JSON error format.|No|

**Table 4: License Query Parameters**

|  **Query Parameter** | **Description** | **Required?** |
|---|---|---|
|  `generalFlags`  | A 4 byte hexadecimal string representing the license flags. ‘0000' is the only allowed value.  | No  |
|  `kek`  | Key Encryption Key (KEK). Keys are stored encrypted with a KEK using a key wrapping algorithm (AES Key Wrap, RFC3394). If `kek` is supplied, either one of the `kid` or the `ek` parameters needs to be supplied, *but not both*.  | No  |
|  `kid`   | A 16 byte hexadecimal string representation of the content encryption key or a string `'^somestring'`. The length of the string followed by the `'^'` cannot be greater than 64 characters.  | No  |
|  `ek`  | A hex string representation of the encrypted content key.  | No  |
|  `contentKey`   | A 16 byte hexadecimal string representation of the content encryption key  | Yes, unless the `kek` and `ek` or `kid` are provided.  |
|  `iv`  | A 16 byte hexadecimal string representation of the content encryption IV  | Yes  |
|  `rentalDuration`  | Duration of the rental in seconds (default - 0)  | No  |
|  `fpExtension`  | A short form wrapping `extensionType` and `extensionPayload`, as a comma separated string. For example: […] `&fpExtension=wudo,AAAAAA==&`[…]  | No, any number can be used  |

**Table 5: Token Restriction Query Parameters**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Query Parameter</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
   <th class="entry"> <b>Required?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> Expiration time of this token. This value MUST be a string in <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> date/time format in the ‘Z' zone designator ("Zulu time"), or an integer preceded by a '+' sign. An example of an RFC 3339 date/time is <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>If the value is a string in <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> date/time format, then it represents an absolute expiration date/time for the token. If the value is an integer preceded by a '+' sign, then it is interpreted as a relative number of seconds, from issuance, that the token is valid. </p> For example, <span class="codeph"> +60 </span> specifies one minute. The maximum and default (if not specified) token lifetime is 30 days. </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Table 6: Correlation Query Parameters**

|  **Query Parameter** | **Description** | **Required?** |
|---|---|---|
|  `cookie`   | An arbitrary string up to 32 characters long, carried in the token and logged by the token redemption server. This can be used to correlate log entries at the redemption server and those at the service provider's servers.  | No  |

**Response**

**Table 7: HTTP Responses**

|  **HTTP Status Code** | **Description** | **Content-Type** | **Entity Body Contains** |
|---|---|---|---|
|  `200 OK`  | No error.  | `text/uri-list`  | License acquisition URL + token  |
|  `400 Bad Request`  | Invalid args  | `text/html` or `application/json`  | Error description  |
|  `401 Unauthorized`  | Auth failed  | `text/html` or `application/json`  | Error description  |
|  `404 Not found`  | Bad URL  | `text/html` or `application/json`  | Error description  |
|  `50x Server Error`  | Server error  | `text/html` or `application/json`  | Error description  |

**Table 8: Event Error Codes**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Code</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> Invalid token expiration time: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> Invalid IP address </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> Invalid content encryption key: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> Invalid output control flags specified: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> Authentication token must be supplied </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> Authentication token invalid: &lt;details&gt; <p>Note:  This can happen if the authenticator is wrong or when accessing the test API at <span class="filepath"> *.test.expressplay.com </span> using the production authenticator and vice versa. </p> <p importance="high">Note:  The Test SDK and Advanced Test Tool (ATT) only work with <span class="filepath"> *.test.expressplay.com </span>, whereas production devices must use <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Insufficient tokens available </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> Missing rights type </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> Invalid rights type </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> Missing rental period end time </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> Missing rental play duration </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> Invalid rental play duration </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> Content encryption key must be 32-hexadecimal digits long </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay Admin error: &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> Service Account Disabled </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Invalid cookie </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> Invalid Output Control, values out of specified range </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> No corresponding value specified </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> Extension type should be 4 characters </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> Extension payload should be Base64 encoded </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag </span> must be encode 4 bytes </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> Invalid error format specified: &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> Device could not be authenticated </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> Invalid token </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> Missing Kid </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Failed to get content key from key storage service </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> kid </span> must be 32 hexadecimal characters long </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> kid </span> must be 64 characters long after the ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> Invalid <span class="codeph"> kid </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> Invalid encrypted key or <span class="codeph"> kek </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Invalid general flags </td> 
  </tr> 
  <tr> 
   <td> -6001 </td> 
   <td> Invalid <span class="codeph"> FPExtension </span> parameters specified </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> Invalid FP Token Type </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> Invalid <span class="codeph"> iv </span> parameter specified </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> Failed to generate CKC for FP </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> Invalid key data specified </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> Service not authorized for FairPlay support </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Invalid rental duration specified </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> Device ID binding is not supported for FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> FairPlay option disabled </td> 
  </tr> 
 </tbody> 
</table>
