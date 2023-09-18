---
title: Enabling Adobe Pass Entitlement Services for a Programer on Xbox 360 and XboxOne Clientless
description: Enabling Adobe Pass Entitlement Services for a Programer on Xbox 360 and XboxOne Clientless
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
---
# Enabling Adobe Pass Entitlement Services for a Programer on Xbox 360 and XboxOne Clientless {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.




1.  The Programmer creates a Zendesk ticket for enabling Xbox 360/One for Adobe Pass Authentication clientless solution by providing the following information:
    
    1.  Platform: e.g. Xbox 360, Xbox One
    
    1.  Requestor ID: e.g. netgeo, CNN etc.

1.  Adobe will create X509 Certificates and configure the private key and the password at its end.

1.  Adobe will provide the Public certificate (of X509 cert) to Programer in the ticket or via email.

1.  The Programmer would then need to install that public certificate at the GDNP portal for the app registered to Microsoft.

1.  The Programmer will then request the JWT (Java Web Token) or STS Token for XboxOne or 360 respectively from the Microsoft Xbox Live service, which would be encrypted using the X509 public certificate provided in step 3.

1.  These are the tokens which contain the unique deviceId for Xbox devices. Include the token (JWT or STS) in the Authorization header using an 'x' parameter as below:
    
    1.  For Xbox 360, the XSTS token must be Base64 encoded before sending to Adobe Pass pay-TV authentication.
    1.  For Xbox One, the JWT is already properly encoded, so no extra encoding should occur. 

1.  All the API calls from the Xbox device should contain the authorization header with the above mentioned token in x parameter.

 

>[!NOTE]
>
>The Xbox in particular has some unique requirements related to digital signing. The Device ID of the XBox console is included in the XSTS token.  For Xbox 360, this is an encrypted SAML assertion; for Xbox One, this is an encrypted JWT. The XBox console app sends the entire XSTS token to Adobe Pass pay-TV authentication. Adobe Pass pay-TV authentication decrypts the token using its public key, parses the token, and extracts the deviceId from it.

>[!NOTE]
>
>Because of the large length of the XSTS token, the XBox console has a technical limitation: it can't send the token as an HTTP GET paramenter to the Adobe Pass pay-TV authentication APIs. To deal with this, Adobe Pass pay-TV authentication allows sending the XSTS token as a part of the HTTP header "Authorization" when calling the APIs. The XSTS token must be encrypted using the public key from the X.509 certificate issued to the Programmer from Adobe Pass pay-TV authentication. Adobe Pass pay-TV authentication stores the associated private key and uses it to decrypt the XSTS token and extract the deviceId from it.
