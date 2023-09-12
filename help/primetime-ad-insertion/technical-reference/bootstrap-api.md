---
title: Bootstrap API
description: Bootstrap API
exl-id: bc7fe244-8664-43ac-b9a1-3967ea8749b1
---
# Bootstrap API {#bootstrap-api}

The Bootstrap API is typically the URL that is sent to the client/video playback APIs.  For options and parameters that can be configured, refer to the [Bootstrap API parameters](#bootstrap-api-parameters).

## Send a command to the Manifest Server {#send-a-command-to-the-manifest-server}

1. Send an `HTTP GET` request for a bootstrap URL constructed using the following pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]
    ?{query parameters}
   ```

   * **File extension** Defined. `.m3u8` if the target manifest are HLS, `.mpd` if the target manifests are in the DASH.

   * **PublisherAssetID** Required. Publisher's unique ID for the specific content.

   * **Content URL** Required. URL of the content M3U8 file, Base64 encoded to be safe within the manifest server URL. The content URL must point to a variant M3U8 file, even if there is only one bit rate stream.

   * **Query parameters** These constitute the most varied part of the request. They tell the manifest server which sort of client is making the request and what it wants the manifest server to do.

   For example:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.[m3u8 or mpd]?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP vs. HTTPS requests**

   The manifest server creates URLs using the same HTTP protocol of the client's request. If a player makes a non-secure HTTP (http) request, the manifest server returns manifest URLs and Auditude tracking URLs with the http protocol. If a player makes a secure HTTP (https) connection, manifest server, it returns manifest URLs and Auditude tracking URLs with the https protocol. 

   >[!NOTE]
   >
   >The manifest server cannot change the protocol (HTTP or HTTPS) of 3rd-party tracking beacons. You must contact the content and 3rd-party ad providers to have them configure the desired protocols.  Segments URL protocols can be changed, however, by default, use the same protocols defined in the target manifests.

## Bootstrap API parameters {#bootstrap-api-parameters}

Query parameters tell the manifest server what sort of client sent the request and what that client wants the manifest server to do. Some are required and some have specific acceptable formats or values.
The complete URL consists of the base URL followed by a question mark, then `parameterName=value` arguments separated by ampersands. For example, `Base URL?name1=value1&name2=value2& . . .&name n=value n`.

The manifest server recognizes the following parameters. All querystring  
parameters are passed to the ad server.

| parameter | description | formats |
|---|---|---|
| _sid_ | A unique id that the manifest server will use to generate the session id. | Required for both DASH/HLS |
| live | Notifies Primetime Ad Insertion that the passed content item is a live stream.  If this parameter is not passed, Primetime Ad insertion will make a secondary request on the initial manifest call to determine if the manifest is live or vod.<br>Possible values:<br>true for live content<br>false for vod content<br>omit for auto-detection | Optional for HLS.  Required for DASH |
| z | The zone id for the asset that needs to be provided to Primetime Ad Insertion. Provided by your Adobe Technical Account Manager. | Required for both DASH/HLS |
| pabimode | Enables [partial ad break insertion](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md#partial-ad-break-support) for Live streams.<br>Possible values:<br>true to enable<br>omit to disable (default disabled) | HLS/DASH |
| ptadtimeout | Enables limiting of overall ad resolution time, if downstream providers take too long to respond.  Long running responses may cause issues with playback, this allows Primetime DAI to force a response within a specific time limit.<br>Possible values:<br>numeric string in milliseconds.<br>omit to disable (default disabled) | HLS/DASH |
| ptadwindow | Duration (in seconds) of the lookback ad decisioning window -- how far back Primetime Ad Insertion will look for ad cues when a DVR user joins the stream. A value of zero will disable mid-roll ad decisioning in the initial manifest, with decisioning resuming only after the first update. This parameter is useful to disable ad insertion into sessions that may only last a few seconds (aka channel flipping).<br>Possible values:<br>numeric string 0-1800 (default 1800) | HLS only |
| ptassetid | Unique ID of the content that is assigned and maintained by publisher.  Required when used in conjunction with the Akamai Ad Scaler. | HLS/DASH |
| ptcdn | List of one or more CDNs to host transcoded assets. For more information, see [Delivery and storage](/help/primetime-ad-insertion/just-in-time-transcoding/delivery-and-storage.md).<br>Possible values:<br>akamai, level3, llnw (limelight networks), comcast.<br>By default, Primetime Ad Insertion CDNs are used. | HLS/DASH |
| ptcueformat | The specified format of tags to perform ad decisioning (for example, scte35).<br>Possible values:<br>dpisimple, dpiscte35, elemental<br>For custom cue formats, contact your technical account representative for the value to use for your use case | HLS/DASH |
| ptfailover | Signals the manifest server to identify primary and failover streams specified in the master playlist, and to treat them as disjoint sets. This facilitates failover and prevents timing errors. (For Apple HLS devices only.) For more information, see [Facilitating HLS player switching](hls-switching-to-failover.md) | HLS only |
| ptmulticall | If enabled, a separate ad request is made for each avail found in a VOD asset.  By default, Primetime Ad Insertion will attempt to collect all available information and send it to the ad server in one request. Possible values:true to enable, <br>omit to disable (default disabled) | HLS/DASH |
| ptparallelstream | Allows customers with players that request CMAF demuxed audio or video streams in parallel to ensure that ads in audio and video tracks are consistent. | HLS only|
| ptprotoswitch | Enables named manifest re-writing rules and ad fetching rules, which will typically be set up by your technical support representative.<br>Example: adfetch_fw, cdn_akm | HLS/DASH |
| pttagds | Enables injection of EXT-X-DISCONTINUITY-SEQUENCE tags into HLS headers.Possible values:true to enableomit to disable (default disabled) | HLS only |
| pttimeline | A string containing the desired timeline for ad placement and content, which overrides ad breaks in the content stream. [ See VOD Timeline Format ] | HLS/DASH |
| pttoken | Enables content fragment/segment authorization token protection schemes for CDNs<br>Possible values:<br>akamai, llnw (limelight), ctl (centurylink) (default tokenization is disabled) | HLS/DASH |
| pttrackingmode | Enable ad tracking schemes.<br>Possible values:<br>simple for client-side ad tracking<br>sstm for server-side ad tracking<br>simplesstm for hybrid client/server ad tracking (by default, no ad tracking is performed) | HLS/DASH |
| pttrackingposition | Instructs the manifest server to return ad tracking information only. Do not specify this parameter in the bootstrap request.<br>Note: The manifest server ignores all passed values. However, if you pass a null or empty string, the manifest server returns the M3U8 | HLS/DASH<br>Client-Side Tracking |
| pttrackingversion | Sets the format version to be returned.<br>Possible values:<br>v1, v2, v3, or vmap | HLS/DASH<br>Client-Side Tracking |
| scteTracking | This parameter indicates to the manifest server that the player fetching the M3U8 needs SCTE tag information to be retrieved.<br>Possible values:<br>true or false (default false)<br>Note: The SCTE-35 data is returned in the JSON sidecar with the following combination of query parameter values:<br>ptcueformat=turner|elemental|nfl|DPIScte35<br>pttrackingversion=v2<br>scteTracking=true<br> | HLS only |
| vetargetmultiplier | The number of segments from the live point The pre-roll offset is configured using: ( vetargetmultiplier * targetduration ) + vebufferlength<br>Note: This parameter applies to Live/Linear HLS streams only<br>Possible values:<br>numeric float<br>(default: 3.0 - same as HLS specification) | HLS only |
| vebufferLength | The number of seconds from the live point, used in conjunction with vetargetmultiplier.<br>Note: This parameter applies to Live/Linear HLS streams only<br>Possible values:<br>numeric float<br>(default: 3.0) | HLS only |
