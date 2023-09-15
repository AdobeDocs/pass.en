---
title: Service Provider Scoping
description: Service Provider Scoping
exl-id: 730c43e1-46c0-4eec-b562-b1ad93cce6d3
---
# Service Provider Scoping {#service-provoider-scoping}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The default implementation of an Adobe Pass authentication integration with an MVPD is based on the **OLCA Specification**. The Authentication Requirements section of the OLCA spec (6.5, Subject Identifier), states that it is possible to indicate the scoping of the Service Provider (SP) for the Subject identifier. (The subject identifier is the obfuscated User ID the MVPD returns to the SP.)  In an Adobe Pass authentication integration, it is required that MVPDs enable scoping of the SP Authentication requests. 

With Adobe Pass authentication taking on the role of SP for the Programmer, it is necessary to implement a customization that enables SP scoping of the Authentication request.  This needs to be done so that the MVPD can identify the network brand passed in the SAML assertion to the MVPD's Identity Provider (IdP).  Scoping can be implemented in one of the two ways described in the next section. 

## Service Provider Scoping {#service-provider-scoping}

Adobe Pass authentication supports the following two ways to enable SP scoping of Authentication requests:

*   **The SAML Issuer Approach.**  In this approach, the "Requestor ID" is appended to the SAML Issuer string in the SAML Authentication request.

*   **The Custom Scoping Property Approach.**  In this approach, the "Requestor ID" is included explicitly as a custom "Scoping" property in the SAML Authentication request.
 
>[!NOTE]
>
>The "Requestor ID" is how Adobe Pass authentication refers to the Programmer's network brand (for example: "CNN" is one of the brands of the Turner network).

### SAML Issuer Approach {#saml-issuer-approach}

This approach uses the SAML `<Issuer>` element in the SAML Authentication request, as shown in this snippet:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
``` 

### Custom Scoping Property Approach {#custom-scoping-property-approach}

This approach uses a custom property named "Scoping", as shown in this snippet of a SAML authentication request:

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->
