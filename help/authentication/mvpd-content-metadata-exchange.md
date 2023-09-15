---
title: MVPD Content Metadata Exchange
description: MVPD Content Metadata Exchange
exl-id: d17e60dc-6c61-4ca2-bad8-1840c95261e0
---
# MVPD Content Metadata Exchange

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#content-metadat-exchange-overview}

This page describes two standard implementations that Adobe Pass authentication uses to send structured data to MVPDs on the Authorization request.  The structured data represents the resource (the Programmer) making the request, and, possibly, additional data such as content rating. 

On the Programmer side, Adobe Pass authentication supports structured MRSS data resources as follows:

1. The Programmer sends the Resource as an MRSS string. Adobe Pass authentication does not encode it on the client side for either web or native devices. The MRSS is sent as a regular string to the Adobe Pass authentication server.
1. On the server side, the MRSS is validated against the predefined schema (http://search.yahoo.com/mrss/).  If the validation passes, Adobe Pass authentication extracts the information from the MRSS fields, including:
    * channel title
    * item title
    * resource identifier
    * rating value and type
1. The values extracted from the MRSS are used to build the authorization request which is passed to the MVPD. 

Adobe Pass authentication supports two approaches for translating the MRSS into formats supported by MVPDs:

* **XACML**.  The first approach aligns with the OLCA standard.  It uses XACML, in which the MRSS values are extracted  to build an XACMLResource with attributes that map to the MRSS elements.  This is then passed to the MVPD.  
* **REST**.  The second approach is REST-based.  The MRSS is base64 encoded and passed as a URL parameter on the REST call.

In both approaches, the MVPD processes the authorization request by including the extracted values inside its own logical flow, and returning an authorization response. 

## Integration Details {#integration-details}

* OLCA-based XACML Structured Resource
* REST-based Structured Resource

### OLCA-based XACML Structured Resource {#olca-based-xacml-struc-resource}

Most Cable-oriented MVPDs use the XACML-based approach, but don't yet support the full structured data approach.  Other MVPDs that support XACML take the Channel Title and accept that for the ResourceID attribute. The example below shows the full structured XACML-based approach. The Adobe Pass authentication team recommends that for MVPDs that use XACML, but don't yet support features like parental controls, they should adapt their XACML integration to the following example:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability

```

### REST-based Structured Resource {#rest-based-struct-resource}

Some MVPDs have standardized on the following REST-based protocol for authorization. This approach is as full featured as the XACML approach, but provides a "lighter weight" implementation.   

`// The MRSS is base64 encoded by Adobe Pass authentication, and passed in that format to the REST-based Authorization endpoint.`
 
`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->
