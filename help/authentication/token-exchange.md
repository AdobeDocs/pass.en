---
title: Exchange a Platform SSO token for an Adobe token
description: Exchange a Platform SSO token for an Adobe token
exl-id: 5ab60268-8f97-4755-8281-be45e812ed7f
---
# Exchange a Platform SSO token for an Adobe token {#exchange-a-platform-sso-token-for-an-adobe-token}

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

Allows a Platform SSO profile to be "exchanged" for an Adobe token.
  
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/tokens/authn | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor (Mandatory)</br>    </br>2.  deviceId (Mandatory)</br>    </br>3.  mvpd (Mandatory)</br>    </br>4.  deviceType (Mandatory)</br>    </br>5.  SAMLResponse (Mandatory)</br>    </br>6.  deviceUser (Deprecated)</br>    </br>7.  appId (Deprecated) | POST | The successful response will be a 204 No Content, indicating that the token was successfully created and is ready to use for the authz flows. | 204 - No Content   </br>400 - Bad request |

  
| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| mvpd | The MVPD Id for which this operation is valid. |
| deviceType | The Apple platform for which we are attempting to obtain a profile-request.  Either **iOS** or **tvOS**. |
| SAMLResponse | The actual profile as returned by Platform SSO. |
| _deviceUser_ | The device user identifier. |
| _appId_ | The application id/name. |
