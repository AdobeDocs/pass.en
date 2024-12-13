---
title: SSO via Passive Authentication
description: SSO via Passive Authentication
exl-id: ce45899f-6e94-4bb0-a2c1-51f03bd66d8d
---
# (Legacy) SSO via Passive Authentication

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

 
## Introduction

The scope of this document is to describe the implementation of the passive authentication flow and how this works with our standard single sign-on approach.

## Usecases

Adobe Pass Authentication enables Single Sign-On (SSO) between apps / sites. After a user logs in with their MVPD credentials, Adobe Pass Authentication generates a secure token that represents the MVPD's authentication session, and binds that token to the user's device using a Device ID. Adobe Pass Authentication stores the token / Device ID either on a server or on the device.

As long as the token is still valid the users will appear directly as being authenticated. This allows users to enter their credentials less frequently while keeping transactions secure.

 

The business use case detailed here is a very specific requirement: that the user MUST be authenticated at least once for every visited site. This enables the MVPD to apply business rules associated with the authN session that may vary per network. It conflicts with the current TVE promise that a user needs to login only once and will be authenticated on all the sites that are part of the Adobe Pass Authentication ecosystem.

 

In order to maintain the business rule but also keep a good user experience, the MVPD DOES NOT require a user to manually supply credential information. We can benefit from the previously set session cookie and attempt to do an automatic re-authentication using the passive flow; from the user perspective he will appear as being logged in automatically.

 

To solve these, we implemented 2 distinct features: authentication per network and passive authentication support. The MVPDs will support SAML passive authN where they are simply re-authenticating a user if an authN session exists on the IdP, regardless on which site that session was created.

 

## Authentication per network

This feature ensures that the MVPD receives an authentication request once for every visited site. This functionality means that an Adobe Pass Authentication authentication token will be bounded to the requestorID, thus being valid only for the network who requested it. As a result, once the user authenticates on site "A" and afterwards visits site "B" it will be required to authenticate.

 

Note that due to the fact that on the MVPD IdP the user is already authenticated, he will not be required to supply login information, but instead the browser will simply be redirected from site "B" to MVPD IdP and then back. The same user will still be authenticated on site "A" if he returns.

 

The following flow depicts the basic Authentication per Network feature:



 

## Passive authentication

The goal for this is to make the re-authentication process happen in the background without the need of a full browser redirect and the picker being shown. As a result a user moving from site A to site B will automatically be authenticated.

 

From an UX perspective there will be no difference between this flow and a flow executed with a regular MVPD. What the user sees is that after entering credentials as a result of visiting site A, it will be automatically authenticated on site B. 

 

In order to make this flow viable the MVPD will need to support passive authentication so that the hidden iframe will not be "stuck" on the login page in the case the MVPD doesn't have a session anymore. This is done via the standard "isPassive" attribute.

 

The following diagram depicts the improved flow and the "behind-the-scenes" passive authentication:



 

SAML request sample
Here's a SAML request sample for the passive authN flow:

 
```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
``` 

## Business rules

MVPDs have specific SSO scoping domain restrictions. For example, only some domains could be allowed by some MVPDs (SSO for the same media company but not across companies).
Some MVPDs might require different authentication rules to be enforced. For example, MVPDs might have different authentication TTLs per different networks. Also, MVPDs might enable home based authentication for some networks but not for others (parental control use cases are strongly represented here).
 

These business requirements should keep in mind that the main use-case is that the user should not be required to sign in again after sucessfully signing in with their MVPD.

This can be accomplished by using authentication per network with passive authN flag. 

 

## Known limitations

iOS – due to the nature of the iOS local storage, SSO flows do not work on iOS for applications developed by different vendors. For more information on SSO in iOS 8 and higher, please refer to this Tech Note.   

 
<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Adobe Pass Authentication Access Enabler
-->
