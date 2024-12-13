---
title: Entitlement Service Monitoring Overview
description: Entitlement Service Monitoring Overview
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
---
# Entitlement Service Monitoring Overview {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#introduction}

TVE sites and apps need to be available 24/7, so customers require real-time insight into entitlement events in order to detect and correct problems as quickly as possible. They also need to analyze monthly data in order to determine which platforms are providing the bulk of the traffic, and which platforms might have a bad implementation and poor conversion rates.

Entitlement Service Monitoring (ESM) provides Programmers and MVPDs wit a data feed that offers real-time visibility into their Authentication and Authorization events. The data is collected from the Adobe Pass Authentication systems, and provided through a RESTful API.  Customers can consume the data in a direct fashion, or from within their own custom-built operational dashboards.

The core elements of the ESM system are its metrics and dimensions. ESM generates reports that contain aggregated metrics according to the dimension selection. As Adobe Pass events are logged in PST timezone, the ESM reports are also available in PST timezone. 

The ESM API is not generally available.  Contact your Adobe representative for availability questions.

## ESM for Programmers {#esm-for-programmers}

### Programmers can monitor the following metrics: {#programmers-monitor-metrics}


| *Metrics Name*          | *Description*            |
|-------------------------|--------------------------|
| authn-attempts |  Number of authentication flows initiated |
|authn-successful | Number of authentication tokens successfully obtained by clients |
|authn-pending | Number of authentication tokens successfully generated (disregarding whether or not the client actually obtained it) |
|authn-failed | Number of failed authentication performed through an external system. |
|clientless-tokens |   Number of Clientless tokens successfully emitted | 
|clientless-failures |  Number of failed attempts to receive tokens from the Clientless API |
|authz-attempts | Number of attempted authorizations |
|authz-successful |  Number of successful authorizations |
|authz-failed |  Number of denied authorizations by MVPDs at application level |
|authz-rejected | Number of authorizations attempts considered to be malicious by Adobe Service Provider and rejected as a result of a DoS attack prevention |
| authz-latency | Total number of milliseconds spent on the MVPD's endpoint | 
| media-tokens | Number of short media tokens generated (which assimilate with the number of play requests) | 
|unique-accounts | Number of unique users who performed entitlement (AuthN / AuthZ) actions in the selected time interval. (This metric will only show if daily values are requested.) </br> This is computed for each individual Data Center. When "dc" dimension is not requested, this metric will not be displayed. | 
| unique-sessions | Number of unique sessions that performed authentication flow calls to the Adobe Pass Authentication service within the selected time interval. (This metric will only show if daily values are requested.) </br> This is computed for each individual Data Center. When "dc" dimension is not requested, this metric will not be displayed. | 
| count | A simple counter used in the event-oriented reports | 

</br>

### Programmers can filter the metrics listed above by the following dimensions: {#progr-filter-metrics}


| *Dimension Name*    | *Description*                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| year                | The 4 digit year                                                                                                                                                                                                                                                                                                                                                                                     | 
| month               | The month of the year (1-12)                                                                                                                                                                                                                                                                                                                                                                         | 
| day                 | The day of the month (1-31)                                                                                                                                                                                                                                                                                                                                                                          | 
| hour                | The hour of the day                                                                                                                                                                                                                                                                                                                                                                                  | 
| minute              | The minute of the hour                                                                                                                                                                                                                                                                                                                                                                               | 
| media-company       | The media company owning the website that initiated the entitlement process for the user                                                                                                                                                                                                                                                                                                             | 
| dc                  | (Data Center) The home region where the request was received.                                                                                                                                                                                                                                                                                                                                        | 
| proxy               | The proxy MVPD (which will be "Direct" for direct integrations)                                                                                                                                                                                                                                                                                                                                      | 
| mvpd                | The MVPD responsible for granting entitlement to the user                                                                                                                                                                                                                                                                                                                                            | 
| requestor-id        | The requestor ID used to perform the entitlement request                                                                                                                                                                                                                                                                                                                                             | 
| channel             | The channel website, extracted from the resource field (extracted from the MRSS payload as the channel/title if provided, or mapped to the resource value if it's not in RSS format).                                                                                                                                                                                                                | 
| resource-id         | The actual resource title involved in the authorization request (extracted from the MRSS payload as the item/title if provided)                                                                                                                                                                                                                                                                      |
| device              | The device platform (PC, mobile, console, etc.)                                                                                                                                                                                                                                                                                                                                                      |
| eap                 | The external authentication provider when authentication flow is performed through an external system. </br> The values can be: </br> - N/A - the authentication was provided by Adobe Pass Authentication </br> - Apple - the external system that provided the authentication is Apple                                                                                                             | 
| os-family           | Operating system running on the device                                                                                                                                                                                                                                                                                                                                                               | 
| browser-family      | User agent used for accessing Adobe Pass Authentication                                                                                                                                                                                                                                                                                                                                              | 
| cdt                 | The device platform (alternative), currently used for Clientless. </br>  The values can be: </br> - N/A - the event did not originate from a Clientless SDK </br> - Unknown - Since the deviceType parameter from a Clientless API is optional, there are calls that do not contain any value. </br> - any other value that was sent through the Clientless API, e.g. xbox, appletv, roku etc. </br> |
| platform-version    | The version of the Clientless SDK                                                                                                                                                                                                                                                                                                                                                                    | 
| os-type             | Operating system running on the device, alternative (not currently used)                                                                                                                                                                                                                                                                                                                             | 
| browser-version     | User agent version                                                                                                                                                                                                                                                                                                                                                                                   | 
| nsdk                | The client SDK used (android, fireTV, js, iOS, tvOS, non-sdk)                                                                                                                                                                                                                                                                                                                                        |
| nsdk-version        | The version of the Adobe Pass Authentication client SDK                                                                                                                                                                                                                                                                                                                                              | 
| event               | The Adobe Pass Authentication event name                                                                                                                                                                                                                                                                                                                                                             | 
| reason              | The reason for failures, as reported by Adobe Pass Authentication                                                                                                                                                                                                                                                                                                                                    | 
| sso-type            | The underlying SSO mechanism: platform/passive/adobe. Indicates that the authorization token was emitted by reusing the AuthN in a different application                                                                                                                                                                                                                                             |
| platform            | The device identified platform. Possible values: </br> - Android </br> - FireTV </br> - Roku </br> - iOS </br> - tvOS </br> - etc                                                                                                                                                                                                                                                                    |
| application-name    | The application name configured, in TVE Dashboard, for the DCR registered application configured to be used.                                                                                                                                                                                                                                                                                         |
| application-version | The application version configured, in TVE Dashboard, for the DCR registered application configured to be used.                                                                                                                                                                                                                                                                                      |
| customer-app        | The custom application id passed via [Device Information](/help/authentication/integration-guide-programmers/legacy/client-information/passing-client-information-device-connection-and-application.md).                                                                                                                                                                                                                                                     |
| content-category    | The category of the content requested by your application.                                                                                                                                                                                                                                                                                                                                           |

## ESM for MVPDs {#esm-for-mvpds}

### MVPDs can monitor the following metrics:

| *Metric Name* | *Description*|
|---|---|
| authn-attempts | Number of authentication flows initiated | 
| authn-successful | Number of authentication tokens successfully obtained by clients |
| authn-pending | Number of authentication tokens successfully generated (disregarding whether or not the client actually obtained it) |
| authn-failed | Number of failed authentication performed through an external system. |
| authz-attempts | Number of attempted authorizations | 
| authz-successful | Number of successful authorizations | 
| authz-failed | Number of denied authorizations by MVPDs at application level | 
| authz-rejected | Number of authorizations attempts considered to be malicious by Adobe Service Provider and rejected as a result of a DoS attack prevention | 
| authz-latency | Total number of milliseconds spent on the MVPD's endpoint | 

### MVPDs can filter the metrics listed above by the following dimensions:

| *Dimension Name* | *Description*                                                                                                                                                                                                                                                                                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| year             | The 4 digit year                                                                                                                                                                                                                                                                                                                                                                                     | 
| month            | The month of the year (1-12)                                                                                                                                                                                                                                                                                                                                                                         | 
| day              | The day of the month (1-31)                                                                                                                                                                                                                                                                                                                                                                          | 
| hour             | The hour of the day                                                                                                                                                                                                                                                                                                                                                                                  | 
| minute           | The minute of the hour                                                                                                                                                                                                                                                                                                                                                                               |
| mvpd             | The mvpd ID used to perform the entitlement request                                                                                                                                                                                                                                                                                                                                                  |
| requestor-id     | The requestor ID used to perform the entitlement request                                                                                                                                                                                                                                                                                                                                             | 
| eap              | The external authentication provider when authentication flow is performed through an external system. </br> The values can be: </br> - N/A - the authentication was provided by Adobe Pass Authentication </br> - Apple - the external system that provided the authentication is Apple                                                                                                             | 
| cdt              | The device platform (alternative), currently used for Clientless. </br>  The values can be: </br> - N/A - the event did not originate from a Clientless SDK </br> - Unknown - Since the deviceType parameter from a Clientless API is optional, there are calls that do not contain any value. </br> - any other value that was sent through the Clientless API, e.g. xbox, appletv, roku etc. </br> |
| sdk-type         | The client SDK used (Flash, HTML5, Android native, iOS, Clientless etc.)                                                                                                                                                                                                                                                                                                                             |
| platform         | The device identified platform. Possible values: </br> - Android </br> - FireTV </br> - Roku </br> - iOS </br> - tvOS </br> - etc                                                                                                                                                                                                                                                                    |
| nsdk             | The client SDK used (android, fireTV, js, iOS, tvOS, non-sdk)                                                                                                                                                                                                                                                                                                                                        |
| nsdk-version     | The version of the Adobe Pass Authentication client SDK                                                                                                                                                                                                                                                                                                                                              | 

## Use Cases {#use-cases}

You can use the ESM data for the following use cases:

- **Monitoring** - Ops or monitoring teams can create a dashboard or chart that calls the API every minute. Using the information displayed they can detect a problem (with Adobe Pass Authentication, or with an MVPD) the minute it appears.  

- **Debugging/Quality Testing** - Because data is also broken down by platform, device, browser, and OS, analyzing usage patterns can pinpoint problems on specific combinations (e.g., Safari on OSX).  

- **Analytics** - The data provided can be used to supplement/audit the client side data being collected through Adobe Analytics or another analytics tool.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
