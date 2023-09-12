---
title: MVPD Authentication
description: MVPD Authentication
exl-id: 9ff4a46e-a37b-414c-a163-9e586252a9c3
---
# MVPD Authentication {#mvpd-authn}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#mvpd-authn-overview}

The actual service provider (SP) role is held by a Programmer, but Adobe Primetime authentication serves as the SP proxy for that Programmer. Using Adobe Primetime authentication as an intermediary allows both MVPDs and Programmers to avoid having to customize their entitlement processes on a case-by-case basis.
               
The steps below present the sequence of events, using Adobe Primetime authentication, when a Programmer requests authentication from an MVPD that supports SAML. Note that the Adobe Primetime authentication Access Enabler component is active on the user's/subscriber's client. From there, the Access Enabler facilitates all steps of the authentication flow.
 
1. When the user requests access to protected content, the Access Enabler initiates authentication (AuthN) on behalf of the Programmer (SP).
1. The SP's app presents an "MVPD Picker" to the user in order to obtain their Pay TV provider (MVPD). The SP then redirects the user's browser to the selected MVPD's identity provider (IdP) service.  This is "**Programmer-initiated Login**".  The MVPD sends the response of the IdP to Adobe's SAML assertion consumer service, where it is processed.
1. Finally, the Access Enabler redirects the browser back to the SP site, informing the SP of the status (success / failure) of the AuthN request.

## The Authentication Request {#authn-req}

As presented in the steps above, during the AuthN flow an MVPD must both accept a SAML-based AuthN request and send a SAML AuthN response.
 
The [Online Content Access (OLCA) Authentication and Authorization Interface Specification](https://www.cablelabs.com/specifications/search?query=&category=&subcat=&doctype=&content=false&archives=false){target=_blanck} presents a standard AuthN request and response. While Adobe Primetime authentication does not require MVPDs to base their entitlement messaging on this standard, looking at the specification can provide insight into the key attributes that are required for an AuthN transaction.
 
>[!NOTE]
>
>The AuthN request an MVPD receives with Adobe Primetime authentication does contain a digital signature. However, the example below does not show a signature, for reasons of brevity. For an example that shows a digital signature, see the example in [the authentication response](#authn-response) in the following sections.
 
Sample SAML authentication request:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

The table below explains the attributes and tags that need to be in an authentication request, with the default expected values.
 
**SAML Authentication request details**

| samlp:AuthnRequest          | &lt;AuthnRequest&gt; issued by Service Provider to Identity Provider.                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | This is the Adobe endpoint to use in subsequent response. Default value: **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer**                                                                                                                                                                                                                                                                                                                                     |
| Destination                 | A URI reference indicating the address to which this request has been sent. This is useful to prevent malicious forwarding of requests to unintended recipients, a protection that is required by some protocol bindings. If it is present, the actual recipient MUST check that the URI reference identifies the location at which the message was received. If it does not, the request MUST be discarded. Some protocol bindings may require the use of this attribute. |
| ForceAuthn                  | The ForceAuthn attribute, if present with a value of true, obligates the identity provider to freshly establish this identity, rather than relying on an existing session it may have with the principal.                                                                                                                                                                                                                                                                  |
| ID                          | An identifier for the request. See [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} section 1.3.4 for details.                                                                                                                                                                                                                                                                                                                                                                                            |
| IsPassive                   | A Boolean value. If "true", the identity provider and the user agent itself MUST NOT visibly take control of the user interface from the requester and interact with the presenter in a noticeable fashion. If a value is not provided, the default is "false".                                                                                                                                                                                                            |
| IssueInstant                | The time instant of issue of the response. The time value is encoded in UTC as described in [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} Section 1.3.3.                                                                                                                                                                                                                                                                                                                                               |
| ProtocolBinding             | A URI reference that identifies a SAML protocol binding to be used when returning the &lt;Response&gt; message. See [SAMLBind] for more information about protocol bindings and URI references defined for them. Default value : urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST                                                                                                                                                                                                  |
| Version                     | The version of this request.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| saml:Issuer                 | Identifies the entity that generated the response message. (For more information on this element, see SAML core 2.0-os  Section 2.2.5)                                                                                                                                                                                                                                                                                                                                     |
| ds:Signature                | An XML Signature that protects the integrity of and authenticates the issuer of the assertion, as described Section  5 in SAML core 2.0-os                                                                                                                                                                                                                                                                                                                                 |
| samlp:NameIDPolicy          | Specifies constraints on the name identifier to be used to represent the requested subject.                                                                                                                                                                                                                                                                                                                                                                                |
| AllowCreate                 | A Boolean value used to indicate whether the identity provider is allowed, in the course of fulfilling the request, to create a new identifier to represent the principal. Default: true                                                                                                                                                                                                                                                                                   |
| Format                      | Specifies the URI reference corresponding to a name identifier format Default: urn:oasis:names:tc:SAML:2.0:nameid-format:transient Adobe recommends: urn:oasis:names:tc:SAML:2.0:nameid-format:persistent                                                                                                                                                                                                                                                                  |
| SPNameQualifier             | Optionally specifies that the assertion subject's identifier be returned (or created) in the namespace of a service provider other than the requester. Default : http://saml.sp.adobe.adobe.com                                                                                                                                                                                                                                                                            |
 
## The Authentication Response {#authn-response}

Having received and handled the authentication request, the MVPD must now send an authentication response.
 
**Sample SAML Authentication Response**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>

```


In the sample above, the Adobe SP expects to fetch the user ID out of the Subject/NameId. The Adobe SP can be configured to get the user ID from a custom defined attribute; the response should contain an element like the following:

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**SAML Authentication response details**
| samlp:Response               | Response received by Adobe Primetime authentication.                                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Destination                  | A URI reference indicating the address to which this request has been sent. This is useful to prevent malicious forwarding of requests to unintended recipients, a protection that is required by some protocol bindings. If it is present, the actual recipient MUST check that the URI reference identifies the location at which the message was received. If it does not, the request MUST be discarded. Some protocol bindings may require the use of this attribute. |
| ID                           | An identifier for the request. It is of type xs:ID and MUST follow the requirements specified in Section 1.3.4 of [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} for identifier uniqueness. The values of the ID attribute in a request and the InResponseTo attribute in the corresponding response MUST match.                                                                                                                                                                                         |
| InResponseTo                 | The ID of a SAML protocol message in response to which an attesting entity can present the assertion. The value must be equal to the one in the ID attribute sent in the Authentication Request. See SAML core 2.0-os                                                                                                                                                                                                                                                      |
| IssueInstant                 | The time instant of issue of the request.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Version                      | The version of the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| saml:Issuer                  | Identifies the entity that generated the request message. (For more information on this element, see Section 2.2.5. SAML core 2.0-os )                                                                                                                                                                                                                                                                                                                                     |
| samlp:Status                 | A code representing the status of the corresponding request.                                                                                                                                                                                                                                                                                                                                                                                                               |
| samlp:StatusCode             | A code representing the status of the activity carried out in response to the corresponding request.                                                                                                                                                                                                                                                                                                                                                                       |
| saml:Assertion               | This type specifies the basic information common to all assertions.                                                                                                                                                                                                                                                                                                                                                                                                        |
| ID                           | The identifier for this assertion.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Version                      | The version of this assertion.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| IssueInstant                 | The time instant of issue of the request.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ds:Signature                 | An XML Signature that protects the integrity of and authenticates the issuer of the assertion, as described Section  5 in SAML core 2.0-os                                                                                                                                                                                                                                                                                                                                 |
| ds:SignedInfo                | The structure of SignedInfo includes the canonicalization algorithm, a signature algorithm, and one or more references. The SignedInfo element may contain an optional ID attribute that will allow it to be referenced by other signatures and objects. See XML-Signature Syntax and Processing                                                                                                                                                                           |
| ds:CanonicalizationMethod    | CanonicalizationMethod is a required element that specifies the canonicalization algorithm applied to the SignedInfo element prior to performing signature calculations. See XML-Signature Syntax and Processing                                                                                                                                                                                                                                                           |
| ds:SignatureMethod           | SignatureMethod is a required element that specifies the algorithm used for signature generation and validation. This algorithm identifies all cryptographic functions involved in the signature operation (e.g. hashing, public key algorithms, MACs, padding, etc.) See XML-Signature Syntax and Processing                                                                                                                                                              |
| ds:Reference                 | Reference is an element that may occur one or more times. It specifies a digest algorithm and digest value, and optionally an identifier of the object being signed, the type of the object, and/or a list of transforms to be applied prior to digesting. See XML-Signature Syntax and Processing                                                                                                                                                                         |
| ds:Transforms                | The optional Transforms element contains an ordered list of Transform elements; these describe how the signer obtained the data object that was digested. The output of each Transform serves as input to the next Transform. The input to the first Transform is the result of dereferencing the URI attribute of the Reference element. The output from the last Transform is the input for the DigestMethod algorithm. See XML-Signature Syntax and Processing          |
| ds:DigestMethod              | DigestMethod is a required element that identifies the digest algorithm to be applied to the signed object. See XML-Signature Syntax and Processing                                                                                                                                                                                                                                                                                                                        |
| ds:DigestValue               | DigestValue is an element that contains the encoded value of the digest. The digest is always encoded using base64. See  XML-Signature Syntax and Processing                                                                                                                                                                                                                                                                                                               |
| ds:SignatureValue            | The SignatureValue element contains the actual value of the digital signature; it is always encoded using base64. See  XML-Signature Syntax and Processing                                                                                                                                                                                                                                                                                                                 |
| ds:KeyInfo                   | KeyInfo is an optional element that enables the recipient(s) to obtain the key needed to validate the signature. See XML-Signature Syntax and Processing                                                                                                                                                                                                                                                                                                                   |
| ds:X509Data                  | An X509Data element within KeyInfo contains one or more identifiers of keys or X509 certificates. See  XML-Signature Syntax and Processing                                                                                                                                                                                                                                                                                                                                 |
| ds: X509Certificate          | The X509Certificate element, which contains a base64-encoded [X509v3] certificate                                                                                                                                                                                                                                                                                                                                                                                          |
| saml:Subject                 | The subject of the statement(s) in the assertion.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| saml:NameID                  | The &lt;NameID&gt; element is of type NameIDType (see Section 2.2.2 in SAML core 2.0-os), and is used in various SAML assertion constructs such as the &lt;Subject&gt; and &lt;SubjectConfirmation&gt; elements, and in various protocol messages.                                                                                                                                                                                                                                           |
| Format                       | A URI reference representing the classification of string-based identifier information.                                                                                                                                                                                                                                                                                                                                                                                    |
| SPNameQualifier              | Further qualifies a name with the name of a service provider or affiliation of providers. This attribute provides an additional means to federate names on the basis of the relying party or parties.                                                                                                                                                                                                                                                                      |
| saml:SubjectConfirmation     | Information that allows the subject to be confirmed. If more than one subject confirmation is provided, then satisfying any one of them is sufficient to confirm the subject for the purpose of applying the assertion.                                                                                                                                                                                                                                                    |
| saml:SubjectConfirmationData | Additional confirmation information to be used by a specific confirmation method. For example, typical content of this element might be a <!--<ds:KeyInfo>--> element as defined in the XML Signature Syntax and Processing specification                                                                                                                                                                                                                                         |
| NotOnOrAfter                 | A time instant at which the subject can no longer be confirmed.                                                                                                                                                                                                                                                                                                                                                                                                            |
| Recipient                    | A URI specifying the entity or location to which an attesting entity can present the assertion. For example, this attribute might indicate that the assertion must be delivered to a particular network endpoint in order to prevent an intermediary from redirecting it someplace else.                                                                                                                                                                                   |
| saml:Conditions              | The &lt;Condition&gt; element serves as an extension point for new conditions.                                                                                                                                                                                                                                                                                                                                                                                                   |
| NotBefore                    | The NotBefore attribute specifies the time instant at which the validity interval begins.                                                                                                                                                                                                                                                                                                                                                                                  |
| saml:AudienceRestriction     | The &lt;AudienceRestriction&gt; element specifies that the assertion is addressed to one or more specific audiences identified by &lt;Audience&gt; elements.                                                                                                                                                                                                                                                                                                                           |
| saml:Audience                | A URI reference that identifies an intended audience.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| saml:AuthnStatement          | An authentication statement.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| AuthnInstant                 | Specifies the time at which the authentication took place.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| SessionIndex                 | Specifies the index of a particular session between the principal identified by the subject and the authenticating authority.                                                                                                                                                                                                                                                                                                                                              |
| saml:AuthnContext            | The context used by the authenticating authority up to and including the authentication event that yielded this statement.                                                                                                                                                                                                                                                                                                                                                 |
| saml:AuthnContextClassRef    | A URI reference identifying an authentication context class that describes the authentication context declaration that follows.                                                                                                                                                                                                                                                                                                                                            |
