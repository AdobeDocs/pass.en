---
title: Check Authentication Flow by Second Screen Web App
description: Check Authentication Flow by Second Screen Web App
exl-id: 5807f372-a520-4069-b837-67ae41b7f79b
---
# Check Authentication Flow by Second Screen Web App {#check-authentication-flow-by-second-screen-web-app}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

This API should be consumed by the second screen login web app to confirm that Adobe Pass Authentication has acknowledged successful login from MVPD. We recommend calling this API before showing a success message to the end user that instructs him/her to proceed to the device console to continue with the workflows.

  
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{registration code} | Login Web App | 1.  registration code  </br>    (Path component)</br>2.  requestor  </br>    (Mandatory) | GET | XML or JSON containing error details if unsuccessful. | 200 - Success   </br>403 - Forbidden |

</br>

| Input Parameter | Description |
| ----------------- | --------------------------------------------------------------------------------------------- |
| registration code | The registration code value supplied by the user at the beginning of the authentication flow. |
| requestor         | The Programmer requestorId for which this operation is valid.                                 |


### Sample Response (in case of an error) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Back to REST API Reference](/help/authentication/rest-api-reference.md)
