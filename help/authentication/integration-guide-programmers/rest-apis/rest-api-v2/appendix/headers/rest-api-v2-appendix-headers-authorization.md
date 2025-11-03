---
title: Header - Authorization
description: REST API V2 - Header - Authorization
exl-id: 86917d7e-ffd9-4d34-8f9c-5a50083f85e6
---

# Header - Authorization {#header-authorization}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>Authorization</b> request header contains the `Bearer` access token required by the client application to access Adobe Pass protected APIs.

For more details about the mechanism to access Adobe Pass protected APIs, refer to the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

## Syntax {#syntax}

<table style="table-layout:auto">
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>Authorization</b>: Bearer &lt;access_token&gt;</td>
   </tr>
   <tr>
      <td>Header Type</td>
      <td>Request header</td>
   </tr>
   <tr>
      <td>Standard</td>
      <td>Yes</td>
   </tr>
</table>

## Directives {#directives}

<b>&lt;access_token&gt;</b>

The access token value is an opaque value having a limited time-to-live (e.g., 24-hours) that must be obtained from Adobe Pass as described in the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) API documentation.

## Examples {#examples}

```JSON
Authorization: Bearer eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI0NmY0MGZiMy01NmJkLTQyYTktOTExYS02YmZmNmEyZmY0
                      MDciLCJuYmYiOjE3MjM1NjE4ODUsImlzcyI6ImF1dGguYWRvYmUuY29tIiwic2NvcGVzIjoiYXBpO
                      mNsaWVudDp2MiIsImV4cCI6MTcyMzU4MzQ4NSwiaWF0IjoxNzIzNTYxODg1fQ.aZUZqwN2fCqNXgX
                      SdKFG9_HcqHjha66G6HmsfTJYcZc12iuLxMu7TT7MbhWVz3kW1jRqgJv8PHhrFSBL5_dgJ1PRSuDg
                      97ZK1secgMKwk46vKZVdtx7LF5t3jGVzQTwN4RqChqyvkW2o67KxVk5xarwJtwB2fwhX_732CYDcv
                      1gWOTLx4xyH5IVvg-P_aImyveG0D-x65I2nOKXaROVvv-kYE6B9OQv_-JBGj72R_yS2AyJQC0R_im
                      0h5S4YvL-c2UZrYK7pvdZq-xAj0uW1wad7PLZjl8yL5CWUz9vzQk2Cmj8adsydjb0u0P3aFrJ0HE9
                      ISqtRvjf4plR1TGWgw6
```
