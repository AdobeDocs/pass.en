---
description: TVSDK takes information from FreeWheel and other ad servers providing VAST responses. FreeWheel provides, within VAST responses, information from the Moat service. The Moat service counts ad impressions with an accuracy that better shows whether creatives capture or neglect an audience's interests.
title: Ad measurements from Moat
exl-id: 20962678-15a0-4e7c-96fd-19c59c5ae008
---
# Ad measurements from Moat{#ad-measurements-from-moat}

TVSDK takes information from FreeWheel and other ad servers providing VAST responses. FreeWheel provides, within VAST responses, information from the Moat service. The Moat service counts ad impressions with an accuracy that better shows whether creatives capture or neglect an audience's interests.

Moat is a service measuring ad viewing across many uses, from browsers to within applications. Moat generates marketing analytics data in real-time across multiple platforms.

The VAST response XML has a property and an element your code can read, the outermost `Ad id` property and the outermost `Extension` element. Either way, your code can use TVSDK to save both the `Ad id` information and the `Extension` information, then organize the information in a tree structure. With this organization, your code can pick up the data from any level and pass it along to wherever it needs to go. The value of the outermost `Ad id` property enables your code to coordinate information from the associated campaign.

For example, FreeWheel can return data in an Extensions element. Below is a sample element.

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 

```

Freewheel can also set the `id` property in the `Ad` element, as shown in the sample below.

```xml
<Ad id="118566" sequence="1">
```

For API information, see the API documentation for the class [NetworkAdInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
