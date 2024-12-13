---
title: Provide MVPD List
description: Provide MVPD List
exl-id: db2d8f19-d0b9-4195-bf0b-f9de0d96062b
---
# (Legacy) Provide MVPD List {#provide-mvpd-list}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

>[!NOTE]
>
> REST API implementation is bounded by [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md)

## REST API Endpoints {#clientless-endpoints}

<REGGIE_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

<SP_FQDN>:

* Production - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Staging - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Description {#description}

Returns list of configured MVPDs for the requestor.

| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| <SP_FQDN>/api/v1/config/{requestorId}</br></br>For example:</br></br><SP_FQDN>/api/v1/config/sampleRequestorId | Adobe Pass Authentication | 1.  Requestor</br>    (Path component)</br>_2.  deviceType (deprecated)_ | GET | XML or JSON containing list of MVPDs. | 200 |

{style="table-layout:auto"}


| Input Parameter | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| requestor       | The Programmer requestorId for which this operation is valid. |
| *deviceType*    | Device Type. |

{style="table-layout:auto"}

### Sample Response {#sample-response}

Same as existing MVPD XML Response to /config servlet

Note: All MVPDs configured to make use of Platform SSO will have the following extra properties within their corresponding node (JSON/XML):

* **enablePlatformServices (boolean):** flag indicating whether this MVPD is integrated via Platform SSO
* **boardingStatus (string):** flag indicating the whether the MVPD fully supports Platform SSO (SUPPORTED) or if the MVPD only appears in the platform picker (PICKER)
* **displayInPlatformPicker (boolean):** should this MVPD appear in the platform picker
* **platformMappingId (string):** the identifier of this MVPD as known by the platform
* **requiredMetadataFields (string array):** the user metadata fields expected to be available on a successful login
