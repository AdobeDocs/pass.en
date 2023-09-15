---
title: MVPD Preflight Authorization
description: MVPD Preflight Authorization
exl-id: da2e7150-b6a8-42f3-9930-4bc846c7eee9
---
# MVPD Preflight Authorization

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#mvpd-preflight-authz-intro}

"Preflight authorization" is a lightweight authorization check for multiple resources. Programmers primarily use it to decorate their UIs (for example, indicating access status with lock and unlock icons). 

Adobe Pass authentication can currently support Preflight Authorization in two ways for MVPDs, either via AuthN response attributes or via a multichannel AuthZ request.  The following scenarios describe the cost / benefit of the different ways that you can implement preflight authorization:

* **Best Case Scenario** - The MVPD provides the list of preauthorized resources during the authorization phase (Multi-channel AuthZ).
* **Worst Case Scenario** - If an MVPD does not support any form of multiple resources authorization, the Adobe Pass authentication server performs an authorization call to the MVPD for each resource in the resources list. This scenario has an impact (proportional to the number of resources) on the response time for the preflight authorization request. It can increase the load on both Adobe & MVPD servers causing performance issues. Also, it will generate authorization requests / responses events without the actual need for a play.
* **Deprecated** - The MVPD provides the list of preauthorized resources during the authentication phase, so there will be no network calls needed, not even the preflight request, since the list is cached on the client.
 
While MVPDs do not have to support preflight authorization, the following sections describe some preflight authorization methods that Adobe Pass authentication can support, before falling back to the worst case scenario above.

## Preflight in AuthN {#preflight-authn}

This preflight scenario is OLCA Compatible (Cableabs). The Authentication and Authorization Interface 1.0 Specification section 7.5.2 titled "Attribute Statement Within Authentication Assertion", describes how a SAML authentication response can contain a list of preauthorized resources. If an IdP supports this, the Adobe Pass authentication server will be able to generate the preflighted resources list at authentication time and cache it on the client along with the Authentication Token. This method also achieves the best case scenario, and no network calls will be performed when the Programmer calls checkPreauthorizedResources(), since everything is already on the client.
 
### Custom Resource List in SAML Attribute Statement {#custom-res-saml-attr}

The IdP's SAML authentication response shall include an AttributeStatement containing resource names that AdobePass should authorize.  Some MVPD's provide this in the following format:

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

The sample above presents a list containing two preauthorized resources: "MMOD" and "Olympics2012".
 
This effectively achieves the best case scenario, and no network calls will be performed when the Programmer calls checkPreauthorizedResources(), since everything is already on the client.

## Multi-channel Preflight in AuthZ {#preflight-multich-authz}

This preflight implementation is also OLCA Compatible (Cablelabs).  The Authentication and Authorization Interface 1.0 Specification (sections 7.5.3 and 7.5.4) describes methods for requesting Authorization information from an MVPD using either SAML Assertions or XACML. This is the recommended way to query authorization status for MVPDs that do not support this as part of the Authentication flow. Adobe Pass authentication issues a single network call to the MVPD to retrieve the list of authorized resources.

 
Adobe Pass authentication receives the list of resources from the Programmer's application. Adobe Pass authentication's MVPD integration can then make one AuthZ call including all those resources, and then parse the response and extract the multiple permit/deny decisions.  The flow for the preflight with multi-channel AuthZ scenario works as follows: 

1. The Programmer's app sends a comma separated list of resources through the preflight client API, for example: "TestChannel1,TestChannel2,TestChannel3". 
1. The MVPD preflight AuthZ request call contains the multiple resources, and has the following structure:

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## Custom Authorization For Multiple Resources {#custom-authz}

Some MVPDs have authorization endpoints that support authorization for multiple resources in one request, but they don't fall under the scenario described in Multi-channel AuthZ. These specific MVPDs require custom work.
 
Adobe can also support multiple channel authorization without changes to the existing implementation.  This approach needs to be reviewed between Adobe and the MVPD technical team to ensure that it works as expected.
 
## MVPDs That Support Preflight Authorization {#mvpds-supp-preflight-authz}

The following table lists the MVPDs that support Preflight Authorization, along with the type of preflight they support and known limitations:
 
|        Preflight Approach       |                                                   MVPD                                                   |                                Notes                               |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| Multi-channel AuthZ             | Comcast AT&T Proxy Clearleap Charter_Direct Proxy GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |                                                                    |
| Channel Lineup in User Metadata | Suddenlink HTC                                                                                           | All Synacor direct integrations can support this approach as well. |
| Fork & Join                     | All others not listed above                                                                              | The default maximum number of resources checked = 5.               |
  
<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
