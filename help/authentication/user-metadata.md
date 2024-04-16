---
title: User Metadata
description: User Metadata
exl-id: 3d7b6429-972f-4ccb-80fd-a99870a02f65
---
# User Metadata {#user-metadata}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/throttling-mechanism.md)

## REST API Endpoints {#clientless-endpoints}

`<REGGIE_FQDN>`:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

`<SP_FQDN>`:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Description {#description}

Retrieve metadata that MVPD shared about the authenticated user.

  
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>`/api/v1/tokens/usermetadata | Streaming App</br></br>or</br></br>Programmer Service | 1.  requestor</br>2.  deviceId (Mandatory)</br>3.  device_info/X-Device-Info (Mandatory)</br>4.  deviceType</br>5.  deviceUser (Deprecated)</br>6.  appId (Deprecated) | GET | XML or JSON containing user metadata or error details if unsuccessful. | 200 - Success<p>404 - No metadata found<p>412 - Invalid AuthN Token (e.g., expired token) |

  
| Input Parameter | Description |
| --- | --- |
| requestor | The Programmer requestorId for which this operation is valid. |
| deviceId | The device id bytes. |
| device_info/<p>X-Device-Info | Streaming Device information.</br></br> **Note:** This MAY be passed device_info as a URL parameter, but due to the potential size of this parameter and limitations on the length of a GET URL, it SHOULD be passed as X-Device-Info n the http header. </br></br> See the full details in [Passing Device and Connection Information](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | The device type (e.g. Roku, PC).</br></br> If this parameter is set correctly, ESM offers metrics that are [broken down per device type](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.</br></br> See [Benefits of using clientless device type parameter in Pass metrics](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md) </br></br> **Note:** The `device_info` replaces this parameter. |
| _deviceUser_ | The device user identifier.</br></br> **Note:** If used, `deviceUser` should have the same values as in the [Create Registration Code](/help/authentication/registration-code-request.md) request. |
| _appId_ | The application id/name. </br></br> **Note:** The `device_info` replaces this parameter. If used, `appId` should have the same values as in the [Create Registration Code](/help/authentication/registration-code-request.md) request. |

>[!NOTE] 
> 
>User metadata information should be available after the authentication flow has completed, but can be updated on the authorization flow, depending on the MVPD and on the metadata type.




## Sample Response {#sample-response}

After a successful call, the server will respond with a XML (default) or JSON object with a structure similar to the one presented below:


```JSON 
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
                         },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
              }
    }
```

At the root of the object there will be three nodes:

* *updated*: specifies an UNIX timestamp that represents the last time the metadata was updated. This property will be set initially by the server when generating the metadata during the authentication phase. Subsequent calls (after the metadata has been updated) will result in an incremented timestamp.
* *data*: contains the actual metadata values.
* *encrypted*: an array listing the encrypted properties. To decrypt a specific metadata value, the Programmer must perform a Base64 decode on the metadata then apply a RSA decryption on the resulting value, using it's own private key (Adobe encrypts the metadata on the server using the Programmer's public certificate).

In case of an error, the server will return a XML or JSON object that specifies a detailed error message.

For more information, see [User Metadata](/help/authentication/user-metadata-feature.md).

[Back to REST API Reference](/help/authentication/rest-api-reference.md)
