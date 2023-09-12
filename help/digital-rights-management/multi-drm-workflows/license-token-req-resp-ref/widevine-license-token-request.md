---
description: The Widevine license token interface provides production and test services.
title: Widevine license token request / response
exl-id: f8d71f63-7783-44f9-8b1b-4b5646dca339
---
# Widevine license token request / response {#widevine-license-token-request-response}

The Widevine license token interface provides production and test services.

This HTTP request returns a token that can be redeemed for a Widevine license.

**Method: GET, POST** (with a www-url-encoded body that contains parameters for both methods)

**URLs:**

* **Production:** `https://wv-gen.{prod_domain}/hms/wv/token` 

* **Test:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **Sample request:** 

  ```
  https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
  <ExpressPlay customer authenticator identifier>
  ```

* **Sample Response:** 

  ```
  https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
  ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**Table 13: Token Query Parameters**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>Query Parameter</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
   <th class="entry"> <b>Required?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>This is your customer API key, one each for your production and test environments. You can find this on the ExpressPlay Admin Dashboard tab. </p> </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> Either <span class="codeph"> html </span> or <span class="codeph"> json </span>. <p>If <span class="codeph"> html </span> (the default) an HTML representation of any errors is provided in the entity body of the response. If <span class="codeph"> json </span> is specified, a structured response in JSON format is returned. See <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON Errors </a> for details. </p> <p>The mime type of the response is either <span class="codeph"> text/uri-list </span> on success, <span class="codeph"> text/html </span> for <span class="codeph"> html </span> error format, or <span class="codeph"> application/json </span> for <span class="codeph"> json </span> error format. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Table 14: License Query Parameters**

| Query Parameter | Description | Required? |
|--- |--- |--- |
|`generalFlags`|A 4 byte hexadecimal string representing the license flags. ‘0000' is the only allowed value|No|
|`kek`|Key Encryption Key (KEK). Keys are stored encrypted with a KEK using a key wrapping algorithm (AES Key Wrap, RFC3394).|No|
|`kid`|A 16 byte hexadecimal string representation of the content encryption key or a string `^somestring'`. The length of the string followed by the `^` cannot be greater than 64 characters. Check note below for an example.|Yes|
|`ek`|A hex string representation of the encrypted content key.|No|
|`contentKey`|A 16 byte hexadecimal string representation of the content encryption key|Yes, unless `kek` and `ek` or `kid` are provided|
|`contentId`|Content Id|No|
|`securityLevel`|Allowed values are 1-5. <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul>|Yes|
|`hdcpOutputControl`|Allowed values are 0, 1, 2. <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul>|Yes|
|`licenseDuration` * |Duration of the license in seconds. If not provided, it indicates that there is no limit to the duration. Please check the note below for detailed information.|No|
|`wvExtension`|A short form wrapping extensionType and extensionPayload, as a comma separated string. See format below. Example: `…&wvExtension=wudo,AAAAAA==&…`|No, any number can be used|

About `licenseDuration`: <ol><li> Playback will stop `licenseDuration` seconds after beginning of playback. </li><li> To allow playback to be stopped/resumed for an unlimited amount of time, omit `licenseDuration` (it will default to infinite). Otherwise specify the amount of time during which end-users should be able to enjoy the stream. </li></ol>

**Table 15: Token Restriction Query Parameters**

| Query Parameter | Description | Required? |
|--- |--- |--- |
|`expirationTime`|Expiration time of this token. This value MUST a string in [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) date/time format in the ‘Z' zone designator ("Zulu time"), or an integer preceded by a + sign. An example of an RFC 3339 date/time is 2006-04-14T12:01:10Z. <br> If the value is a string in [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) date/time format, then it represents an absolute expiration date/time for the token. If the value is an integer preceded by a + sign, then it is interpreted as a relative number of seconds, from issuance, that the token is valid. For example, `+60` specifies one minute. <br> The maximum and default (if not specified) token lifetime is 30 days.|No|

**Table 16: Correlation Query Parameters**

|  **Query Parameter** | **Description** | **Required?** |
|---|---|---|
|  `cookie`  | Arbitrary string up to 32 characters long carried in the token and logged by the token redemption server. Can be used to correlate log entries at the redemption server and those at the service provider's servers.  | No  |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**Table 17: HTTP Response**

|  **HTTP Status Code** | **Description** | **Content-Type** | **Entity Body Contains** |
|---|---|---|---|
|  `200 OK`  | No error.  | `text/uri-list`  | License acquisition URL + token  |
|  `400 Bad Request`  | Invalid args  | `text/html` or `application/json`  | Error description  |
|  `401 Unauthorized`  | Auth failed  | `text/html` or `application/json`  | Error description  |
|  `404 Not found`  | Bad URL  | `text/html` or `application/json`  | Error description  |
|  `50x Server Error`  | Server error  | `text/html` or `application/json`  | Error description  |

**Table 18: Event Error Codes**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> Code </th> 
   <th class="entry"> Description </th> 
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
   <td> Authentication token invalid: &lt;details&gt; <p>Note:  This can happen if the authenticator is wrong or when accessing the test API at *.test.expressplay.com using the production authenticator and vice versa. </p> <p importance="high">Note:  The Test SDK and Advanced Test Tool (ATT) only work with <span class="filepath"> *.test.expressplay.com </span>, whereas production devices must use <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> Insufficient tokens available </td> 
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
   <td> Missing <span class="filepath"> kid </span> </td> 
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
   <td> <span class="codeph"> kid </span> must be 64 characters long after the '^' </td> 
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
   <td> -6005 </td> 
   <td> Invalid key data specified </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> Invalid rental duration specified </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Device ID binding is not supported for Widevine </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> Missing security level value </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> Invalid security level value </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> Missing HDCP output control value </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> Invalid license duration specified </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> Failed to generate Widevine license </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> Invalid <span class="codeph"> WVExtension </span> parameters specified </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Widevine option disabled </td> 
  </tr> 
 </tbody> 
</table>
