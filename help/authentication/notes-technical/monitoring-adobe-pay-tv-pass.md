---
title: Monitoring Adobe Pass Authentication
description: Monitoring Adobe Pass Authentication
exl-id: fb000e9d-b5aa-45b1-a914-9e419ec8a4d9
---
# Monitoring Adobe Pass Authentication {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

Customers can use [Nagios](http://www.nagios.org) or other tools to check whether Adobe Pass Authentication is up or down. 

## Monitoring Endpoints {#monitoring-endpoints}

### Endpoints that you can monitor {#endpoints-to-monitor}

*   The configuration endpoint for all platforms: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- It is available over either HTTP or HTTPS (depending upon the choice made by the content provider's developer). If this endpoint is missing that means that your content will not be available across all platforms and all MVPDs. For the Clientless REST API we have also the following endpoint:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

*   The following endpoints are part of the Adobe Pass Authentication web SDK.  If it is missing it means that pay-TVpass is down for all Programmers and all web properties:
    
    * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
    * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### Endpoints that you should not monitor {#endpoints-not-monitor}

*   `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

    You will always get a 503 error, because this endpoint needs an MVPD SAML response on it.

*   Other Entitlement endpoints - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

You cannot monitor these endpoints because they need a payload for a relevant reply.
