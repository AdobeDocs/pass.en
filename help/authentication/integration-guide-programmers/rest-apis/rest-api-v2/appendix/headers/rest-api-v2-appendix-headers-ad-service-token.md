---
title: Header - AD-Service-Token
description: REST API V2 - Header - AD-Service-Token
exl-id: 856f76fc-cde6-4b3f-81f7-deaa0df015dc
---
# Header - AD-Service-Token {#header-ad-service-token}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>AD-Service-Token</b> request header contains the unique user identifier as `JWS` obtained from an identity service running outside of Adobe Pass Authentication systems.

This header is designed for use in single sign-on (SSO) enabled flows leveraging the Service Token method.

For more details about the single sign-on (SSO) enabled flows leveraging the Service Token method, refer to the [Single sign-on using service token flows](../../flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md) documentation.

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AD-Service-Token</b>: &lt;unique_user_identifier&gt;</td>
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

<b>unique_user_identifier</b>

The JSON Web Signature (`JWS`) which is a signed JSON Web Token (`JWT`) containing unique user identifier information.

The `JWT` has the following attributes:

<table>
   <tr>
      <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>iss</td>
      <td>The unique identifier associated with the entity that offers the application an external identity service to achieve single sign-on (SSO).</td>
   </tr>
   <tr>
      <td>sub</td>
      <td>The unique identifier for the user as returned by the external identity service.</td>
   </tr>
   <tr>
      <td>aud</td>
      <td>The audience, which should be "Adobe".</td>
   </tr>
   <tr>
      <td>iat</td>
      <td>The issued at timestamp for the present JWT.</td>
   </tr>
   <tr>
      <td>exp</td>
      <td>The expiration timestamp for the present JWT.</td>
   </tr>
</table>

The `JWT` must be signed using `SHA256withRSA` algorithm.

The `JWT` must be signed with a private key, part of a pair of RSA private key - public key managed by the external identity service.

The public key of that pair must be handed over to Adobe Pass Authentication in order to be able to recognise `JWT` tokens signed with the aforementioned private key.

## Examples {#examples}

```JSON
// JWT
// Header
// {
//  "alg": "RS256",
//  "kid": "qapEaY0hYNvphytwII3Sae_cAKyLS7GZOqtT_a4ajeo"
// }
// Payload data
// {
//  "sub": "Jane",
//  "name": "Jane Smith",
//  "iat": 1516239022,
//  "iss": "adobe",
//  "exp": 1720152820,
//  "aud": "adobe",
//  "jti": "3b2fb040-30a9-43d7-b647-d00ac495bab"
// }
 
// JWS
// eyJhbGciOiJSUzI1NiIsImtpZCI6InFhcEVhWTBoWU52cGh5dHdJSTNTYWVfY0FLeUxTN0daT3F0VF9hNGFqZW8ifQ.eyJzdWIiOiJKYW5lIiwibmFtZSI6IkphbmUgU21pdGgiLCJpYXQiOjE1MTYyMzkwMjIsImlzcyI6ImFkb2JlIiwiZXhwIjoxNzIwMTUyODIwLCJhdWQiOiJhZG9iZSIsImp0aSI6IjNiMmZiMDQwLTMwYTktNDNkNy1iNjQ3LWQwMGFjNDk1YmFiIn0.stHLZFh-635LDNjv9HRHzq912ICNCVGUS3f4RS_bAxpUiUSB6CShS2VvU4V-THEXj7d_zk1mxtPP0QM_pCrh4Vk2GaPRa856Bt_PhsfQY-_benDcB6MIoFX67qrREGncGiv7JEs3ksa-P1YvBYXolT7t52K093kFaQtICfB-aBa8danRZvUrJHjjFoILEpTbQuzxKRN6y36J3p1FZ-SfDuofHp3SnXDrWFRYyXYQnb9WFlhNBxR400-0vzTONZYd097WWy1shMw5V8TvIDvCDE5ifqk31gMdYga-N3JkcTA5QoW7Zl80UV7BhR5v14Va1IZLcbFra_UJdEzbBwW_nA

AD-Service-Token: eyJhbGciOiJSUzI1NiIsImtpZCI6InFhcEVhWTBoWU52cGh5dHdJSTNTYWVfY0FLeUxTN0daT3F0VF9hNGFqZW8ifQ.eyJzdWIiOiJKYW5lIiwibmFtZSI6IkphbmUgU21pdGgiLCJpYXQiOjE1MTYyMzkwMjIsImlzcyI6ImFkb2JlIiwiZXhwIjoxNzIwMTUyODIwLCJhdWQiOiJhZG9iZSIsImp0aSI6IjNiMmZiMDQwLTMwYTktNDNkNy1iNjQ3LWQwMGFjNDk1YmFiIn0.stHLZFh-635LDNjv9HRHzq912ICNCVGUS3f4RS_bAxpUiUSB6CShS2VvU4V-THEXj7d_zk1mxtPP0QM_pCrh4Vk2GaPRa856Bt_PhsfQY-_benDcB6MIoFX67qrREGncGiv7JEs3ksa-P1YvBYXolT7t52K093kFaQtICfB-aBa8danRZvUrJHjjFoILEpTbQuzxKRN6y36J3p1FZ-SfDuofHp3SnXDrWFRYyXYQnb9WFlhNBxR400-0vzTONZYd097WWy1shMw5V8TvIDvCDE5ifqk31gMdYga-N3JkcTA5QoW7Zl80UV7BhR5v14Va1IZLcbFra_UJdEzbBwW_nA
```
