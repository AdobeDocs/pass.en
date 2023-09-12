---
description: The PlayReady license token interface provides production and test services.
title: PlayReady license token request / response
exl-id: 12f925f7-336b-42b2-95a9-e806801bab8c
---
# PlayReady license token request / response {#playready-license-token-request-response}

The PlayReady license token interface provides production and test services.

This HTTP request returns a token that can be redeemed for a PlayReady license.

**Method: GET, POST** (with a www-url-encoded body that contains parameters for both methods)

**URLs:**

* **Production:** `https://pr-gen.{prod_domain}/hms/pr/token` 

* **Test:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **Sample request:** 

  ```
  <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
   <ExpressPlay customer authenticator identifier>
   &kid=<CEKSID>
   &contentKey=<CEK>
   &rightsType=BuyToOwn
   &analogVideoOPL=0
   &compressedDigitalAudioOPL=0
   &compressedDigitalVideoOPL=0
   &uncompressedDigitalAudioOPL=0
   &uncompressedDigitalVideoOPL=0
  </xref href="https:>
  ```

* **Sample Response:** 

  ```
  {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
              "token":"<base64-encoded ExpressPlay token>"}
  ```

## Request Query Parameters {#section_26F8856641A64A46A3290DBE61ACFAD2}

**Table 9: Token Query Parameters**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Query Parameter</b> </th> 
   <th class="entry"><b>Description</b> </th> 
   <th class="entry"><b>Required?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>This is your customer API key, one each for your production and test environments. You can find this on the ExpressPlay Admin Dashboard tab. </p> </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>Either <span class="codeph"> html</span> or <span class="codeph"> json</span>. If <span class="codeph"> html</span> (the default) an HTML representation of any errors is provided in the entity body of the response. <p>If <span class="codeph"> json</span> is specified, a structured response in JSON format is returned. See <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON Errors</a> for details. </p> <p>The mime type of the response is either <span class="codeph"> text/uri-list</span> on success, <span class="codeph"> text/html</span> for HTML error format, or <span class="codeph"> application/json</span> for JSON error format. </p> </td> 
   <td> No </td> 
  </tr> 
 </tbody> 
</table>

**Table 10: License Query Parameters**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Query Parameter</b> </th> 
   <th class="entry"><b>Description</b> </th> 
   <th class="entry"><b>Required?</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>A 4 byte hexadecimal string representing the license flags. It must be set to ‘00000001' for a persistent license. <p>Note: Rental licenses (<span class="codeph"> rightsType=Rental</span>) MUST be persistent. </p> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> Key Encryption Key (KEK). Keys are stored encrypted with a KEK using a key wrapping algorithm (AES Key Wrap, RFC3394). </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kid</span> </td> 
   <td>A 16 byte hexadecimal string representation of the content encryption key or a string <span class="codeph"> ^somestring'</span>. The length of the string followed by the '^' cannot be greater than 64 characters. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> A hex string representation of the encrypted content key. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> A 16 byte hexadecimal string representation of the content encryption key </td> 
   <td>Yes, unless <span class="codeph"> kek</span> and <span class="codeph"> ek</span> or <span class="codeph"> kid</span> are provided </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>Specifies the kind of rights. Must be <span class="codeph"> BuyToOwn</span> or <span class="codeph"> Rental</span>. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>Rental end date. This value MUST be in the ‘RFC 3339' _ date/time format in the ‘Z' zone designator ("Zulu time") format, or an integer preceded by a '+' sign. <p>If the value is a <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> date/time format, then it represents an absolute expiration date/time for the license. An example of an RFC 3339 date/time is 2006-04-14T12:01:10Z. </p> <p> If the value is an integer preceded by a '+' sign, it is taken as a relative number of seconds from the time the token is issued. The content cannot be played after this time. Only valid if <span class="codeph"> rightsType</span> is <span class="codeph"> Rental</span>. </p> </td> 
   <td>Yes, when <span class="codeph"> rightsType</span> is <span class="codeph"> Rental</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>Time, in seconds, that the content can be played once play has started. Only valid if <span class="codeph"> rightsType</span> is Rental. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> Integer value to indicate the Output Protection Level for analog video. Valid range 0-999. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> Integer value to indicate the Output Protection Level for compressed digital audio. Valid range 0-999. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> Integer value to indicate the Output Protection Level for compressed digital video. Valid range 0-999. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> Integer value to indicate the Output Protection Level for uncompressed digital audio. Valid range 0-999. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> Integer value to indicate the Output Protection Level for uncompressed digital video. Valid range 0-999. </td> 
   <td> Yes </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>Required behaviour when the output is unknown. Allowed values: <span class="codeph"> Allow</span>, <span class="codeph"> Disallow</span> or <span class="codeph"> SDOnly</span> </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> A 4-byte hex value to indicate the flags for other output control options </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>An arbitrary 4-letter word representing a 32-bit identifier for an Extension. Each letter's 8-bit ASCII code is the corresponding 8-bit byte portion of the identifier. For example, the identifier value 0x61626364 (hexadecimal) would be written ‘<span class="codeph"> abcd</span>', because the ASCII code for ‘a' is 0x61, etc. </td> 
   <td> No </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> A base64 encoded string of the Extension. </td> 
   <td>Yes, when <span class="codeph"> extensionType</span> is specified. </td> 
  </tr> 
 </tbody> 
</table>

## Responses {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**Table 11: HTTP Responses**

| **HTTP Status Code** |**Description** |**Content-Type** |**Entity Body Contains** |
|---|---|---|---|
| `200 OK`  | No error.  | `text/uri-list`  | License acquisition url and token  |
| `400 Bad Request`  | Invalid args  | `text/html` or `application/json`  | Error description  |
| `401 Unauthorized`  | Auth failed  | `text/html` or `application/json`  | Error description  |
| `404 Not found`  | Bad URL  | `text/html` or `application/json`  | Error description  |
| `50x Server Error`  | Server error  | `text/html` or `application/json`  | Error description  |

**Table 12: Event Error Codes**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>Code</b> </th> 
   <th class="entry"><b>Description</b> </th> 
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
   <td>Authentication token invalid: &lt;details&gt; <p>Note:  This can happen if the authenticator is wrong or when accessing the test API at *.test.expressplay.com using the production authenticator and vice versa. </p> <p importance="high">Note: The Test SDK and Advanced Test Tool (ATT) only work with <span class="filepath"> *.test.expressplay.com</span>, whereas production devices must use <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> must be encode 4 bytes </td> 
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
   <td> -4018 </td> 
   <td>Missing <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> Failed to get content key from key storage service </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> kid</span> must be 32 hexadecimal characters long </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> kid</span> must be 64 characters long after the ^ </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>Invalid <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>Invalid encrypted <span class="codeph"> key</span> or kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> Invalid unknown output type error </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> PlayReady option is disabled for this service </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> Invalid general flags </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> Device ID must be 32 hexadecimal characters long </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> Invalid device ID </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> Missing OPL value </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>Only one of <span class="codeph"> kek</span> or <span class="codeph"> contentKey</span> can be specified </td> 
  </tr> 
 </tbody> 
</table>
