---
title: Header - AP-Visitor-Identifier
description: REST API V2 - Header - AP-Visitor-Identifier
exl-id: 216f398b-1cfa-4453-a81d-963675b33ec2
---
# Header - AP-Visitor-Identifier {#header-ap-visitor-identifier}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>AP-Visitor-Identifier</b> request header contains the `ECID` required by the client application to uniquely identify a visitor across Adobe Experience Cloud solutions.

For more details about the usage of ECID in Adobe Pass Authentication, refer to the [Using Experience Cloud ID in Adobe Pass Authentication](../../../../features-premium/analytics/exp-cloud-id-authn.md) documentation.

## Syntax {#syntax}

<table style="table-layout:auto">
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AP-Visitor-Identifier</b>: &lt;visitor_identifier&gt;</td>
   </tr>
   <tr>
      <td>Header Type</td>
      <td>Request header</td>
   </tr>
   <tr>
      <td>Standard</td>
      <td>No</td>
   </tr>
</table>

## Examples {#examples}

```JSON
AP-Visitor-Identifier: "THE_ECID_VALUE"
```
