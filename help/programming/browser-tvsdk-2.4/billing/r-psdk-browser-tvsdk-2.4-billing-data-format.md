---
description: Browser TVSDK sends billing metrics to Adobe in an XML format.
title: Transmit billing metrics
exl-id: f6ed72be-a5a8-48f2-b518-76c710300ea7
---
# Transmit billing metrics{#transmit-billing-metrics}

Browser TVSDK sends billing metrics to Adobe in an XML format.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

If you use a network capture tool to monitor the statistics Browser TVSDK transmits to Adobe, you should see units like the following:

```
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

The boolean properties `drmProtected`, `adsEnabled`, and `midrollEnabled` appear only if they are true.
