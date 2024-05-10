---
title: Proxy MVPD Web Service
description: Proxy MVPD Web Service
exl-id: f75cbc4d-4132-4ce8-a81c-1561a69d1d3a
---
# Proxy MVPD web service {#proxy-mvpd-wbservice}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.
>In order to use the Proxy MVPD web service, you will need to: 
>- ask the support team for a software  statement for your registered application
>- obtain an access token based on [Dynamic Client Registration](dynamic-client-registration.md)
> 

>[!NOTE]
>
>In order to use the Proxy MVPD web service, you will need to: 
>- ask the support team for a software  statement for your registered application
>- obtain an access token based on [Dynamic Client Registration](dynamic-client-registration.md)
> 

## Overview {#overview-proxy-mvpd-webserv}

A "Proxy MVPD" is an MVPD that, in addition to managing its own integration with Adobe Pass Authentication, also manages the entitlement process on behalf of a group of associated "Proxied MVPDs". This arrangement is transparent to Programmers. 

To implement the ProxyMVPD feature, Adobe Pass Authentication provides RESTful web services, with which ProxyMVPDs can submit and retrieve lists of ProxiedMVPDs. The protocol used for this public API is REST HTTP, with the following assumptions:

– The Proxy MVPD uses the HTTP GET method to retrieve the list of the current integrated MVPDs.
– The Proxy MVPD uses the HTTP POST method to update the list of the supported MVPDs.

## Proxy MVPD services {#proxy-mvpd-services}

– [Retrieve proxied MVPDs](#retriev-proxied-mvpds)
– [Submit proxied MVPDs](#submit-proxied-mvpds)

### Retrieve proxied MVPDs {#retriev-proxied-mvpds}

Retrieves the current list of Proxied MVPDs integrated with the Proxy MVPD identified.

| Endpoint                                                                 | Called By | Request Parameters    | Request Headers           | HTTP Method | HTTP  Response                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|--------------------------------------------------------------------------|-----------|-----------------------|---------------------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| &lt;FQDN&gt;/control/v3/mvpd-proxies/&lt;proxy-mvpd-identifier&gt;/mvpds | ProxyMVPD | proxy-mvpd-identifier | Authorization (Mandatory) | GET         | <ul><li> 200 (ok) - The request was successfully processed, and the response contains a list of ProxiedMVPDs in XML format</li><li>401 (unauthorized) - Indicates one of the following:<ul><li>The client MUST request a new access_token</li><li>The request originates from an IP address that is not present in the allowed list</li><li>The token is not valid</li></ul></li><li>403 (forbidden) - Indicates either that the operation is not supported for the provided parameters, or the proxy MVPD is not set as a proxy or is missing</li><li>405 (method not allowed) - An HTTP method other than GET or POST was used. Either the HTTP method is unsupported generally, or is unsupported for this specific endpoint.</li><li>500  (internal server error) – An error has been raised on the server side during the request process.</li></ul> |

Curl example:

`curl -X GET -H "Authorization: Bearer <access_token_here>" "https://mgmt-prequal.auth-staging.adobe.com/control/v3/mvpd-proxies/ProxyMVPD_Adobe/mvpds"`
 

XML Response example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### Submit proxied MVPDs {#submit-proxied-mvpds}

Pushes an array of MVPDs integrated with the Proxy MVPD identified.

|                                 Endpoint                                 | Called By | Request Parameters    |                   Request Headers                   | HTTP Method |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  HTTP Response                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|:------------------------------------------------------------------------:|:---------:|-----------------------|:---------------------------------------------------:|:-----------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;FQDN&gt;/control/v3/mvpd-proxies/&lt;proxy-mvpd-identifier&gt;/mvpds | ProxyMVPD | proxy-mvpd-identifier | Authorization (Mandatory) proxied-mvpds (Mandatory) |    POST     | <ul><li>201 (created) - The push was successfully processed</li><li>400 (bad request) - The server doesn't know how to process the request:<ul><li>Incoming XML does not adhere to schema published in this specification</li><li>The proxied mvpds do not have unique ids</li><li>The pushed requestorIds do not exist Other Servlet container reason for 400 response code</li></ul><li>401 (unauthorized) - Indicates one of the following:<ul><li>The client MUST request a new access_token</li><li>The request originates from an IP address that is not present in the allowed list</li><li>The token is not valid</li></ul></li><li>403 (forbidden) - Indicates either that the operation is not supported for the provided parameters, or the proxy MVPD is not set as a proxy or is missing</li><li>405 (method not allowed) - An HTTP method other than GET or POST was used. Either the HTTP method is unsupported generally, or is unsupported for this specific endpoint.</li><li>500 (internal server error) – An error has been raised on the server side during the request process.</li></ul> |

Curl example:

`curl -X POST -H "Authorization: Bearer <access_token_here>" "https://mgmt-prequal.auth.adobe.com/control/v3/mvpd-proxies/ProxyMVPD_Adobe/mvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`

 

XML example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```
 

### Posting Frequency {#posting-frequency}

Adobe Pass Authentication recommends that ProxyMVPDs should push their list of ProxiedMVPDs only when there is a change from the previous push. 

### Deleting Proxied MVPDs {#delete-proxied-freqency}

If the ProxyMVPD pushes an XML record with an empty ProxiedMVPDs list, that empty list will be stored in our system just like any list, thus effectively deleting the previous list.

 

## XSD Format {#xsd-format}

Adobe has defined the following accepted format for posting/retrieving proxied MVPDs from/to our public web service:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Notes on elements:**

–   `id` (mandatory) - The Proxied MVPD ID must be a string relevant to the name of the MVPD, using any of the following characters (as it will be exposed to Programmers for tracking purposes):
    –   Any alphanumeric characters, underscore ("_"), and hyphen ("-"). 
    –   The idID must conform to the following regular expression:
        `(a-zA-Z0-9((-)|_)*)`

        Thus it must have at least one character, start with a letter, and continue with any letter, digit, dash, or underscore.

–   `iframeSize` (optional) - The iframeSize element is optional and defines the size of the iFrame if the MVPD authentication page is supposed to be in an iFrame. Otherwise, if the iframeSize element is not present, the authentication will happen in a full browser redirect page.
–   `requestorIds` (optional) - The requestorIds values will be provided by Adobe. A requirement is that a proxied MVPD should be integrated with at least one requestorId. If the "requestorIds" tag is not present on the proxied MVPD element, then that proxied MVPD will be integrated with all available requestors integrated under the Proxy MVPD.
–   `ProviderID` (optional) - When the ProviderID attribute is present on the id element, the value of ProviderID will be sent on the SAML authentication request to the Proxy MVPD as the Proxied MVPD / SubMVPD ID (instead of the id value). In this case, the value of id will be used only in the MVPD picker presented on the Programmer page, and internally by Adobe Pass Authentication. The length of the ProviderID attribute must be between 1 and 128 characters.
 
## Security {#security}

For a request to be considered valid, it must respect the following rules:

– The request header must contain the security Oauth2 access token from [Dynamic Client Registration](dynamic-client-registration.md).
– The request must come from a specific IP address that is has been allowed.
– The request must be sent over the SSL protocol. 

Any parameters present in the request header that are not listed above will be ignored. 

Curl example:

`curl -X GET -H "Authorization: Bearer <access_token_here>" "https://mgmt-prequal.auth-staging.adobe.com/control/v3/proxiedMvpds"`

## Proxy MVPD Web Service Endpoints for the Adobe Pass Authentication Environments {#proxy-mvpd-wevserv-endpoints}

– **Production URL:** https://mgmt.auth.adobe.com/control/v3/proxiedMvpds
– **Staging URL:** https://mgmt.auth-staging.adobe.com/control/v3/proxiedMvpds
– **PreQual-Production URL:** https://mgmt-prequal.auth.adobe.com/control/v3/proxiedMvpds
– **PreQual-Staging URL:** https://mgmt-prequal.auth-staging.adobe.com/control/v3/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Pass Authentication glossary](/help/authentication/glossary.md)
-->
