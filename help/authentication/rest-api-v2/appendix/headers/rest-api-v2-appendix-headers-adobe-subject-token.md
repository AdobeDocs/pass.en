---
title: Header - Adobe-Subject-Token
description: REST API V2 - Header - Adobe-Subject-Token
---

# Header - Adobe-Subject-Token {#header-adobe-subject-token}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>Adobe-Subject-Token</b> request header contains the unique platform identifier as `JWS` or `JWE` obtained from an identity service or library running outside of Adobe Pass Authentication systems.

This header is designed for use in single sign-on (SSO) enabled flows leveraging the Platform Identity method.

For more details about the single sign-on (SSO) enabled flows leveraging the Platform Identity method, refer to the [Single sign-on using platform identity flows](../../flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md) documentation.

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>Adobe-Subject-Token</b>: &lt;unique_platform_identifier&gt;</td>
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

<b>unique_platform_identifier</b>

The JSON Web Signature (`JWS`) or JSON Web Encryption (`JWE`) which is a signed or encrypted JSON Web Token (`JWT`) containing unique platform identifier information.

This is available for the following platforms:

* [Amazon](../../../amazon-fireos-sso-using-clientless-api-cookbook.md)

## Examples {#examples}

Please see the examples as described for the following platforms:

* [Amazon](../../../amazon-fireos-sso-using-clientless-api-cookbook.md)
