---
description: There are some security considerations to be aware for Browser TVSDK.
title: Security considerations
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
---
# Security considerations{#security-considerations}

There are some security considerations to be aware for Browser TVSDK.

* **Adobe Flash Player**

  * Flash Player does not allow access to data that resides outside the domain from which the SWF originated.

    To allow access, host a cross domain policy file with appropriate permissions at the root of the server that is hosting the data. In Flash Fallback mode in Browser TVSDK (Flash Player version 23 and higher), you need the authorization token for your domain. To generate the token, contact your Adobe representative.

* **JavaScript**

  * JavaScript follows the same origin policy and prevents access to resources across domain boundaries.

    To allow access to these resources, the Access-Control-Allow-Origin (CORS) header must be set on the resources that are hosted on origins other than the player. Optionally, if the content is specified by using byte ranges, the CORS pre-flight options request must indicate that these requests are allowed by the origin.

* **Browsers and mixed content**

  * Browsers require that AES-128 encrypted content be hosted over secure Origin (for example, HTTPS).

    Since most browsers do not allow mixed content, we recommend that the player, the content, and the associated assets such as Key/ WebVTT files are also hosted over secure Origin.     
    
    >[!IMPORTANT]
    >
    >Starting in version 2.4.5, if the player is hosted over HTTPS, Browser TVSDK converts the HTTP calls to HTTPS when using MSE technology.
