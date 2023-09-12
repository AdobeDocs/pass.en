---
title: Manifest Server Debugging Tool
description: Manifest Server Debugging Tool
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
---

# Manifest Server Debugging Tool {#manifest-server-debugging-tool}

The debugging tool enables publishers to investigate potentially costly ad insertion problems by examining debugging information returned in real time by the manifest server in HTTP headers or, when more detailed information is needed, examining session logs after the fact. Adobe partners like Akamai can use the tool to debug their integrations with Primetime ad decisioning.

The tool supports debugging ad insertion problems in any of the main manifest server ad tracking configurations:

* Client-side tracking with a player based on TVSDK.
* Client-side tracking with a player not based on TVSDK.
* Server-side tracking.

To support all of these cases, the tool does not require or use player publisher codes.

When you initiate a manifest server session, you can set a parameter on the request URL to ask it to log debugging information. Using different values of that parameter, you can also ask the manifest server to return specified pieces of debugging information in HTTP headers, but headers can contain only a limited amount of information. You can obtain credentials from Adobe to access complete log files, which the manifest server saves periodically (for example, hourly) on an archive server. Once you have credentials for that server, you can access it directly at any time.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Debugging tool options {#debugging-tool-options}

When invoking the debugging tool, you have several options for what information the manifest server returns in HTTP headers. The options do not affect what the manifest server places in log files.

### Specifying ptdebug {#specifying-ptdebug}

When initiating debug logging for a manifest server session, you can add the ptdebug parameter to the request URL to specify the following options for the information that the manifest server returns in HTTP headers:

* ptdebug=true All records except `TRACE_HTTP_HEADER` and most `call/response data` from `TRACE_AD_CALL` records.
* ptdebug=AdCall Only TRACE_AD_*type* (for example, TRACE_AD_CALL) records.
* ptdebug=Header Only TRACE_HTTP_HEADER records.

The options do not affect what the manifest server places in the log files. You have no control of that, but the log files are text files, so you can apply a wide variety of tools to extract and reformat the information that interests you.

Here is an example of the HTTP header returned when `ptdebug=Header`. Some long strings of hex digits are replaced by `. . .` for clarity.

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## Formats of log records {#formats-of-log-records}

Each log record has a type and a set of fields, some of which might be optional. The fields of all records up to the record type are the same. They provide a timestamp and information about the session. The record type identifies the kind of event being logged, and subsequent fields provide information about the logged event.

The structure of a log record is as follows:

`datetime request_id session_id zone_id record_type` *other fields.*

|Field|Type|Description|
|--- |--- |--- |
|datetime|string|Timestamp|
|request_id|string|Request ID used by the manifest server (unix timestamp)|
|session_id|string|Session ID used by the manifest server|
|zone_id|integer|Zone ID|
|record_type|string|Type of event being logged|
|other fields|***|Depend on type of event|

### TRACE_REQUEST_INFO records {#trace-request-info-records}

Records of this type log the results of HTTP requests. Fields beyond TRACE_REQUEST_INFO appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|request_method|string|HTTP method (GET or POST)|
|request_uri|string|HTTP request URI (without host)|
|request_length|integer|Length of request (bytes)|
|response_length|integer|Length of response (bytes)|
|delta|integer|Time (milliseconds) to process request|
|module_type|string|Variant, Stream, or VOD|
|remote_address_aud_client_ip|string|(see note)|
|remote_address_x_fwd_for_hdr_key|string|(see note)|
|remote_host_port|string|(see note)|

>[!NOTE]
>
>The last three fields are optional.

An example:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383

```

### TRACE_HTTP_HEADER records {#trace-http-header-records}

Records of this type log HTTP headers exchanged during HTTP calls between the manifest server and client, ad server, or content server. Fields beyond TRACE_HTTP_HEADER appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|request_type|string|Type of request (MAIN or UNKNOWN)|
|request_response|string|Response header (request or response)|
|header_name|string|HTTP header name|
|header_value|string|Base64-encoded HTTP header value|

>[!NOTE]
>
>The request_type and header_value fields are optional.

An example:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACE_AD_CALL records {#trace-ad-call-records}

Records of this type log the results of manifest server ad requests. Fields beyond TRACE_AD_CALL appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|request_duration|integer|Time (milliseconds) from request to response|
|ad_server_query_url|string|URL for the ad call, including query parameters|
|ad_system_id|string|Ad system, from the ad server response (Auditude if not specified)|
|avail_id|string|ID of the avail, from the ad cue in the content manifest file (N/A for VOD)|
|avail_duration|number|Duration (seconds) of the avail, from the ad cue in the content manifest file (N/A for VOD)|
|ad_server_response|string|Base64-encoded response from ad server|

An example:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .

```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE, and TRACE_AD_REDIRECT records {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

Records of this type log the results of the ad requests indicated by the record type. Fields beyond the record type appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|avail_id|string|ID of the avail, from the ad cue in the content manifest file (live) or from the manifest server (VOD)|
|ad_type|string|Type of ad (DIRECT or REDIRECT)|
|ad_duration|integer|Duration (seconds) of ad, from ad server response|
|ad_content_url|string|URL of the ad's manifest file, from the ad server response|
|ad_content_url_actual|string|URL of the inserted ad's manifest file. Empty for TRACE_AD_REDIRECT.|
|ad_system_id|string|Ad system, from the ad server response (Auditude if not specified)|
|ad_id|string|ID of the ad, from the ad server response|
|creative_id|string|ID of the creative, from the ad node, from the ad server response|
|ad_call_id|string|Not used. Reserved for future use.|
|delta|integer|Time (milliseconds) taken by this event|
|misc|string|Reason ad was skipped|

>[!NOTE]
>
>The ad_content_url_actual, ad_call_id, and misc fields are optional.

For TRACE_AD_RESOLVE and TRACE_AD_INSERT, the URL in the ad_content_url_actual field is for the transcoded ad if one is available. Otherwise the field is empty for TRACE_AD_RESOLVE or the same as ad_content_url for TRACE_AD_INSERT.

An example:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA

```

### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond TRACE_TRACKING_URL appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|pts|number|Program timestamp. Time within video to call the URL.|
|ad_system|string|Ad system (auditude or freewheel)|
|url|string|URL pinged|
|status|string|HTTP status returned from the ping|

An example:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE records {#trace-transcoding-no-media-to-transcode-records}

Records of this type log a missing ad creative. The only field beyond TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE appears in the table.

|Field|Type|Description|
|--- |--- |--- |
|ad_id|string|Fully qualified ad ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOL: AUDITUDE,VAST)|

### TRACE_TRANSCODING_REQUESTED records {#trace-transcoding-requested-records}

Records of this type log the results of transcoding requests that the manifest server sends to CRS. Fields beyond TRACE_TRANSCODING_REQUESTED appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|ad_id|string|Fully qualified ad ID|
|ad_manifest_url|string|URL of the ad's manifest file, from the ad server response|
|creative_type|string|Type of media|
|flags|string|ID3 indicates whether the transcoding request includes a request to add an ID3 tag|
|target_duration|string|Target duration (seconds) of the transcoded creative|

### TRACE_TRACKING_REQUEST records {#trace-tracking-request-records}

Records of this type indicate a request to do server side tracking. Fields beyond TRACE_TRACKING_REQUEST appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|tracking_url_count|integer|Number of tracking URLs|
|start|float|PTS fragment start time (seconds with millisecond precision)|
|end|float|PTS fragment end time (seconds with millisecond precision)|

### TRACE_TRACKING_REQUEST_URL records {#trace-tracking-request-url-records}

Records of this type provide a tracking URL for server side tracking. Fields beyond TRACE_TRACKING_REQUEST_URL appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|timestamp|float|Time (seconds, with precision .001) within the playback session to ping the tracking URL|
|ad_system|string|Ad system (for example, auditude)|
|url|string|URL to ping|

### TRACE_WEBVTT_REQUEST records {#trace-webvtt-request-records}

Records of this type log requests the manifest server makes for WEBVTT captions. Fields beyond TRACE_WEBVTT_REQUEST appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|vtt_uri|string|URL for request|
|start|float|Split start time (seconds with millisecond precision)|
|end|float|Split end time (seconds with millisecond precision)|

### TRACE_WEBVTT_RESPONSE records {#trace-webvtt-response-records}

Records ``of ``this ``type ``log ``responses ``the ``manifest ``server ``sends ``to ``clients ``in `` `answer` ``to ``requests `` `for` ``WEBVTT ``captions. Fields beyond TRACE_WEBVTT_RESPONSE ``appear in the order shown in the table, separated `by`tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|response|string|Base64-encoded response sent to client|

### TRACE_WEBVTT_SOURCE records {#trace-webvtt-source-records}

Records of this type log responses to requests the manifest server makes for WEBVTT captions. Fields beyond TRACE_WEBVTT_SOURCE appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|Returned HTTP status code|
|source|string|Base64-encoded original VTT content|


### TRACE_MISC records {#trace-misc-records}

Records of this type enable the manifest server to log events and information not otherwise planned for when it ingests ads. The field beyond TRACE_MISC consists of a message string. Messages that might appear include the following:

* Ad ignored :AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*seconds*, ignore=*ignore*, redirectAd=*redirectAd*, priority=*priority*
* Ad placement returned null.
* Ad successfully stitched.
* Ad call failed : *error message*.
* Adding User-Agent to fetch raw manifest: *user-agent*.
* Adding cookie to fetch raw manifest: [cookie]
* Bad URL *requested URL error message*. (Failed to parse variant URL)
* Called url: URL *got return: response code*. ( Live URL)
* Called url: URL *return code: response code*. ( VOD URL)
* Conflict found while resolving ads: either one of - mid-roll start or mid-roll end falls within pre-roll or pre-roll contained in mid-roll (VOD).
* Detected unhandled exception thrown by the handler for URI: *request URL*.
* Done generating variant manifest. (Variant)
* Done generating variant manifest.
* Exception in handling VAST redirect *redirect URL *error: *error message*.
* Failed to fetch ad's playlist for *ad manifest URL*.
* Failed to generate targeted manifest. (HLSManifestResolver)
* Failed to parse first ad call response: *error message*.
* Failed to process *GET|POST *request for path: *request URL*. (Live/VOD)
* Failed to process live manifest request: *request URL*. (Live)
* Failed to return a variant manifest: *error message*.
* Failed to validate group ID: *group ID*.
* Fetching raw manifest: *content URL*. (Live)
* Following VAST redirect: *redirect URL*.
* Found empty avails. (VOD)
* Found *number *ads. (VOD)
* HTTP request received. (Very first message)
* Ignoring ad because difference between ad response duration (*ad response duration *sec) and actual ad duration (*actual duration *sec) is larger than the limit. (HLSManifestResolver)
* Ignoring avail that provided no ID value. (GroupAdResolver.java)
* Ignoring avail that provided invalid time value: *time *for availId = *avail ID*.
* Ignoring avail that provided invalid duration value: *duration *for availId = *avail ID*.
* Initialize new session. (Variant)
* Invalid HTTP method. It must be a GET. (VOD)
* Invalid HTTP method. Tracking request must be a GET. (Live)
* Invalid URL *requested URL error message*. (Variant)
* Invalid group. (HLSManifestResolver)
* Invalid request. Caption is not a valid tracking request. (VOD)
* Invalid request. Caption request must be made after session is established. (VOD)
* Invalid request. Tracking request must be made after session is established. (VOD)
* Invalid server instance for overload group ID: *group ID*. (Live)
* Limit of VAST redirects reached - *number*.
* Making ad call: *ad call URL*.
* No manifest found for: *content URL*. (Live)
* No matching avail found for avail ID: *avail ID*. (HLSManifestResolver)
* No playback session found. (HLSManifestResolver)
* Processing VOD request for manifest *content URL*.
* Processing variant.
* Processing caption request for manifest *content URL*.
* Processing tracking request. (VOD)
* Redirect ad response empty. ( VASTStAX)
* Requesting: *URL*.
* Returning error response for GET request because no playback session was found. (VOD)
* Returning error response for GET request because of an internal server error.
* Returning error response for GET request specifying an invalid asset: *ad request ID*. (VOD)
* Returning error response for GET request specifying an invalid or empty group ID: *group ID*. (VOD)
* Returning error response for GET request specifying an invalid tracking position value. (VOD)
* Returning error response for GET request with invalid syntax - *request URL*. (Live/VOD)
* Returning error response for request with unsupported HTTP method: *GET|POST*. (Live/VOD)
* Returning manifest from cache. (VOD)
* Server is overloaded. Proceed without ad stitch request. (Variant)
* Start generating targeted manifest. (HLSManifestResolver)
* Start generating variant manifest from: *content URL*. (Variant)
* Start stitching ads into manifest. (VODHLSResolver)
* Trying to stitch ad at `HH:MM:SS`: AdPlacement \[adManifestURL=*ad Manifest URL*, durationSeconds=*seconds*, ignore=*ignore*, redirectAd=*redirect ad*, priority=*priority*.\]
* Unable to get ads because of invalid pttimeline - returned the content without ads. (VOD)
* Unable to get ads - returned the content without ads. (VOD)
* Unable to get ad query and no content URL was given. (VOD)
* Valid URL received. (VOD/Variant)
* Variant M3U8 not found. (Variant)

### TRACE_TRACKING_URL records {#trace-tracking-url-records-1}

The manifest server generates records of this kind after calling a tracking URL during the server side tracking workflow. Fields beyond TRACE_TRACKING_URL appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|pts|number|PTS time within stream|
|ad_system|string|Ad's ad system (auditude or freewheel)|
|url|string|URL pinged|
|state|string|HTTP status code|

### TRACE_PLAYBACK_PROGRESS records {#trace-playback-progress-records}

The manifest server generates records of this kind when it receives a signal about playback progress during the server side tracking workflow. Fields beyond TRACE_PLAYBACK_PROGRESS appear in the order shown in the table, separated by tabs.

|Field|Type|Description|
|--- |--- |--- |
|status|string|HTTP status code|
|bandwidth|integer|Bandwidth of the stream|
|pts|integer|PTS time within stream|
|ms_time|integer|Time when manifest server generated tracking URL|
|url|string|Redirect URL|
|header_user_agent|string|HTTP User-Agent header|
|header_dnt|integer|HTTP do-not-track header|
|effective_remote_address|string|IPv4 effective remote address|
|remote_address|string|IPv4 remote address|

>[!NOTE]
>
>The last four fields are optional.

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://helpx.adobe.com/support/primetime.html) page.
