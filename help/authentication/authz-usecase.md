---
title: MVPD Authorization
description: MVPD Authorization
exl-id: 215780e4-12b6-4ba6-8377-4d21b63b6975
---
# MVPD Authorization

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#mvpd-authz-overview}

Authorization (AuthZ) is performed via back-channel (server-to-server) communications between an Adobe-hosted backend server and the MVPD AuthZ endpoint. 

For AuthZ requests, the authorization endpoint should be able to process at least the following parameters:

* **Uid**. The user ID received from the authentication step.

* **Resource ID**. A string identifying a given content resource. This resource ID is specified by the Programmer, and the MVPD must reinforce the business rules on these resources (for example, by checking that the user is subscribed to a certain channel).

In addition to determining whether the user is authorized, the response must include the time-to-live (TTL) of this authorization, that is when the authorization expires. If the TTL is not set, the AuthZ request will fail.  For this reason, **the TTL is a mandatory configuration setting on the Adobe Pass authentication side**, in order to cover the case when an MVPD does not include the TTL in their request.  

## The Authorization Request {#authz-req}

An AuthZ request must include a subject on whose behalf the request is being made, the resource(s) that the subject is trying to access, the action that the subject is trying to perform on the resource, and the environment in which the operation is about to take place. In the particular case of Adobe Pass authentication, these elements correspond to:

| XACML element | Corresponds to                                                                                                                 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Subject       | The principal identified by the Authenticated Session, referenced by the 'subject-token' AttributeValue of the SAML assertion. |
| Resource      | A URI for the Protected Resource.                                                                                              |
| Action        | VIEW.                                                                                                                          |
| Environment   | Includes IP address of the requesting client, as seen by the SP.                                                               |

 

The SP at this point must prepare an XACML Authorization DecisionQuery and send it (via HTTP POST) to the (previously-agreed-upon) Policy Decision Point (PDP) for the IdP. Below is an example of a simple XACML Request (see XACML core spec):

```XML

POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```
 

After receiving the AuthZ request, the MVPD's PDP evaluates the request and determines whether the subject should be allowed to perform the requested action on the resource. The MVPD then returns a response with a Decision, Status code, and message, as described in The Authorization Response below.

## The Authorization Response {#authz-response}

The response to the AuthZ request comes after the MVPD evaluates the request and applies the requested business rules to determine if the subject is allowed to perform the requested action on the resource . The returned Response to Adobe Pass authentication is expressed again following the XACML core spec with a Decision, a Status code, message, and Obligations that the SP has as the Policy Enforcement Point (PEP). The following is a sample Response:

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

The following is a list of DENY Obligations that Adobe Pass authentication supports and enables Programmers to fulfill:

* **urn:tve:xacml:2.0:obligations:restrict-pc** - The Subscriber has failed a parental control check and the SP must take appropriate measures to restrict access to this content.

* **urn:tve:xacml:2.0:obligations:upgrade** - The Subscriber does not have an appropriate subscription level.  Must upgrade subscription in order to access content. 

Adobe Pass authentication supports the following **PERMIT** Obligations and enables Programmers to fulfill them:

* **urn:cablelabs:olca:1.0:obligations:log** – Adobe Pass logs the transaction and can make available via the agreed-upon reporting mechanism.

* **urn:cablelabs:olca:1.0:obligations:re-authz** – Adobe Pass authentication refreshes the authorization again in n seconds (specified as an argument to the Obligation via a XACML AttributeAssignment – see XACML core spec , Section 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
