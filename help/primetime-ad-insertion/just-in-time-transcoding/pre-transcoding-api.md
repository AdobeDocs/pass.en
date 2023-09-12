---
title: Pre-Transcoding API
description: You can use the just-in-time repackaging API to transcode ad creatives ahead of time, so an content-compatible versions are available when needed, eliminating the 2-4 minute delay associated with just-in-time (JIT) repackaging.
exl-id: d45668e0-ec8a-4e5a-a56b-cffff27561f2
---
# Pre-transcoding and re-packaging API {#pre-transcoding-api}

Primetime Ad Insertion offers a pre-transcoding API for situations where creative URLs are known in advance, such as for large direct-sold events.  This eliminates the 2-4 minute delay associated with just-in-time transcoding.

## HTTP Request {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Send an HTTP POST command to the specified URL to tell CRS which ad creative you want transcoded and which options you'd like it to use. The response code reports success or failure and other information.

This request requires a username and password. You can obtain these from your Adobe technical account manager. If you need information about authenticating, contact your Adobe Primetime Enablement representative.

To submit a transcoding request to CRS, send an HTTP message as follows:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Method -** `POST` 

* **Auth -** `Digest` 

* **Header -** `Content-Type: text/xml` 

* **Body -** XML as in the following example: 

  ```xml
  <RepackageList>
      <Repackage>
          <AdSystem>Auditude</AdSystem>
          <AdID>AUD1</AdID>
          <CreativeID>AUD-CR1</CreativeID>
          <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
          <Zone>3</Zone>
      </Repackage>
      <Repackage>
          <AdSystem>Auditude</AdSystem>
          <AdID>AUD2</AdID>
          <CreativeID>AUD-CR1</CreativeID>
          <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
          <Format>id3 targetdur=5</Format>
          <Zone>3</Zone>
      </Repackage>
  </RepackageList>
  ```

The `RepackageList` block in the Body can contain 1 to 300 `Repackage` blocks. If the number of `Repackage` blocks in the Body exceeds 300, then the HTTP Request will fail with the following error: 

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


The required and optional parameters in a `Repackage` block are as follows:

* **`AdSystem`** (Required) - The source ad server, for example, `Auditude`, `FreeWheel`, `Apad.tv`. This is a string value that corresponds to the VAST element `AdSystem`. 

* **`AdId`** (Required) - This is an identifier for the 3rd party ad server specified in the request. It corresponds to the `id` attribute of the `Ad` element in a VAST response. 

* **`CreativeURL`** (Required) - The location (URI) of the ad creative to be transcoded. This corresponds to the VAST `MediaFile` element. 

* `CreativeID` (optional) - The identifier for the ad creative that is to be included as part of ad-experience. 
* **`Zone`** (Required) - Zone ID for your account (obtain from your technical account manager). This is a numerical value that corresponds to the Auditude platform `publisher_site_id` setting. 

* **`Format`** (optional) - Parameters to control how CRS transcodes the ad creative:

   * `clientside` - Generate output compatible with the URL that TVSDK uses to communicate with the CDN.     
    
    >[!IMPORTANT]
    >
    >You must provide this parameter if you want the repackaged ad to be compatible with Client Side Ad Insertion. If you do not provide this, the repackaged ad will only be compatible with Server Side Ad Insertion.

    * `hls` - Generate an HLS-compatible transcoded ad creative. 
    * `dash` - Generate a DASH-compatible transcoded ad creative. 
    * `id3` - Inject ID3 timed metadata tags into the transcoded ad creative. 
    * `targetdur` - Segment duration (in seconds) for the transcoded ad creative. Default is `targetdur=4`. This value should correspond to the value specified in the manifest for `<s>` in the target duration tag: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >DASH-compatible assets are not compatible with Adobe Primetime ad insertion.

>[!IMPORTANT]
>
>To ensure smoothest playback, set `targetdur` to match the content chunk duration.

## HTTP Response {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS responds to the request with one of the following status codes:

* **HTTP 202** - Accepted (with empty body). This indicates success. CRS uploads the transcoded ad to the CDN server. 
* **HTTP 400** - Bad Request. The posted XML is invalid. 
* **HTTP 500** - Internal Server Error. The server encountered an internal problem (for example, the server was unable to connect to a database).

## Pre-transcoding assets for SSAI or CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Using the repackaging API, you can pre-transcode future SSAI or CSAI events. If the assets are intended to be used with SSAI in future, make sure that all the parameters in the POST calls are unique. The parameters are: AdSystem, AdId, CreativeURL, Zone, Format. Any differences in this set of parameters, result in a new transcoding request for SSAI.

For assets used with CSAI in the future, the asset uniqueness depends on Zone and CreativeURL. AdSystem and AdId do not result in different transcoded assets and these are available to clients.
