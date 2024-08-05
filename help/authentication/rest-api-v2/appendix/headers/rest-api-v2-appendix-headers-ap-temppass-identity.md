---
title: Header - AP-TempPass-Identity
description: REST API V2 - Header - AP-TempPass-Identity
---

# Header - AP-TempPass-Identity {#header-ap-temppass-identity}

## Overview {#overview}

The <b>AP-TempPass-Identity</b> request header contains the user identity information used to achieve promotional TempPass.

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AP-TempPass-Identity</b>: &lt;user_identity_information&gt;</td>
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

<b>&lt;user_identity_information&gt;</b>

The `Base64-encoded` value over the user identity information associated with the end user to which a promotional temporary access needs to be granted.

## Examples {#examples}

```JSON
// Identity
// {"email": "example@domain.com"}

// Base64-encoded
// eyJlbWFpbCI6ICJleGFtcGxlQGRvbWFpbi5jb20ifQ==

AP-TempPass-Identity: eyJlbWFpbCI6ICJleGFtcGxlQGRvbWFpbi5jb20ifQ==
```
