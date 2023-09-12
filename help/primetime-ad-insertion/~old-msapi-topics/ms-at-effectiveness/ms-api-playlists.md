---
description: The manifest server returns master playlists in M3U8 format, conforming to the proposed HTTP Live Streaming standard. It consists of a set of variant transport streams (TSs), each containing renditions of the same content for different bit rates and formats. Adobe Primetime ad insertion adds the EXT-X-MARKER directive tag, to be interpreted by client video players.
title: EXT-X-MARKER Directive
---

# EXT-X-MARKER Directive {#ext-x-marker-directive}

The manifest server returns master playlists in M3U8 format, conforming to the proposed HTTP Live Streaming standard. It consists of a set of variant transport streams (TSs), each containing renditions of the same content for different bit rates and formats. Adobe Primetime ad insertion adds the EXT-X-MARKER directive tag, to be interpreted by client video players.

For details on the EXT-X-MARKER tag, see [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>This functionality is only available if the bootstrap manifest server URL does not contain the `pttrackingmode` parameter.

>[!NOTE]
>
>The EXT-X-MARKER tag is added to ad segments and not content segments.

The draft standard at [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) describes the contents and format of variant playlists. The EXT-X-MARKER tag directs the client to invoke a callback. It contains the following components: 

* **ID** Unique identifier (string) for this callback event within the context of the program stream.

* **TYPE** Type (string) of the callback event: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd, or AdBegin

* **DURATION** Length of time (in seconds) from the start of the segment carrying the tag for which the directive remains valid.

* **OFFSET** Optional. The offset (in seconds) relative to the beginning of the segment playback, when the callback must be invoked.

  * `PodBegin` and `PrerollPodBegin` contain beacon information in the DATA attribute and are fired at start of the segment. So the `OFFSET` tag is not available here. 
    
  * `AdBegin` contains beacon information in the DATA attribute and impression tags are fired at start of that segment. So the `OFFSET` tag is not available here either. 
    
  * `PodEnd` and `PrerollPodEnd` contain beacon information in the DATA attribute but are fired at end of the current segment because these tags are expected to be fired at end of last segment of last ad in the pod. In this case, `OFFSET` is set to `<duration of segment>` to specify that the beacon be fired at end of the current segment.

* **DATA** Base64-encoded string enclosed in double quotes containing the data to pass to the application when invoking the callback. It contains ad tracking information that conforms to VMAP1.0 and VAST3.0 specifications.

* **COUNT** Number of ads that will be stitched in the ad break.

  Only Applicable if the TYPE component is set to PodBegin or PrerollPodBegin.

* **BREAKDUR** Total duration (in seconds) of the filled ad break.

  Only Applicable if the TYPE component is set to PodBegin or PrerollPodBegin.

When constructing the callback, interpret the EXT-X-MARKER components as follows:

* When the tag contains `OFFSET`, fire the callback at the specified offset relative to the beginning of content playback in that segment. Otherwise, fire the callback as soon as the content in that segment starts playing. 
* Use `DURATION` to track the ad content's progress and to request URLs for tracking events. 
* Pass `ID`, `TYPE`, and `DATA` to the callback.

Use the `PrerollPodBegin`, and `PrerollPodEnd` values for `TYPE` to decide which TS segment to play first in live/linear streams. 

>[!NOTE]
>
>The `PrerollPodBegin`, and `PrerollPodEnd` values are only available when a pre-roll ad is inserted into a live stream.

The manifest server includes EXT-X-MARKER tags in the following segments:

* The first segment in the ad break, to track the beginning of an ad pod. 
* The first segment of the ad, to track the start/complete/progress of an individual ad within an ad pod. 
* The last segment in the ad break, to track the end of an ad pod.

The manifest server sends a `VMAP1.0-conformant` XML document to track the start and end of each ad break. It is a filtered version of the actual VMAP1.0 response returned by the ad server, and primarily contains the tracking events as shown here: 

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

For each ad creative the manifest server inserts into the program content, it sends a VAST3.0-conformant XML document to track that ad. Each XML document contains an `<InLine>` element describing the linear ad creative inserted, or a `<Wrapper>` element in the case of wrapper ads (that is, linked or redirected ads), and any associated companion ads and extensions. If the VAST response contains a sequence attribute, such as when the ad is part of an ad pod, the document includes that attribute. The following is a sample VAST3.0-conformant XML document for tracking an individual ad: 

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 

```