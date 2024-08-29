---
title: Header - AP-Device-Identifier
description: REST API V2 - Header - AP-Device-Identifier
exl-id: 90a5882b-2e6d-4e67-994a-050465cac6c6
---
# Header - AP-Device-Identifier {#header-ap-device-identifier}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>AP-Device-Identifier</b> request header contains the streaming device identifier as it was created by the client application.

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AP-Device-Identifier</b>: &lt;type&gt; &lt;identifier&gt;</td>
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

## Directives {#directives}

<b>&lt;type&gt;</b>

The device identifier type.

There is only one supported types as presented below.

<table>
   <tr>
      <th style="background-color: #EFF2F7; width: 15%;">Type</th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td>fingerprint</td>
      <td>The device identifier consists of an opaque identifier and is created by the client application.</td>
   </tr>
</table>


<b>&lt;identifier&gt;</b>

The `Base64-encoded` value of the device identifier.

## Example {#example}

```JSON
// device identifier
// ba23d141-d715-561c-94f4-e9e4c966b1eb

// Base64-encoded
// YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi

AP-Device-Identifier: fingerprint YmEyM2QxNDEtZDcxNS01NjFjLTk0ZjQtZTllNGM5NjZiMWVi
```
