---
title: Integrating Adobe Pass authentication server side data into Adobe Analytics
description: Integrating Adobe Pass authentication server side data into Adobe Analytics
exl-id: c1f1f2a3-c98c-4aed-92ad-1f9bfd80b82b
---
# Integrating Adobe Pass Authentication server side data into Adobe Analytics

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted. 

Customers of Adobe Pass Authentication want to see the Adobe Pass authentication (Adobe Pass) server side data in Adobe Analytics dashboard for easier consumption.

The data will serve to track important TVE metrics such authentication conversion rates per MVPD, unique users based on the MVPD User ID and more.

It is not meant to replace a client side implementation if one exists already since the user activity cannot be tracked beyond the specific events below in the absence of a visitor ID. If the customers are providing a visitor ID on Pass calls then we can unlock another type of Analytics integration - real time - that can join all the Pass events with the existing customer data, more details on this new type of possible integration here: "[Using Experience Cloud ID in Adobe Pass Authentication](/help/authentication/exp-cloud-id-authn.md)"

## Metrics included {#metrics-included-int-authn-analyt}

| Event                      | Description                                                                                                          |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| AuthN requested            | Number of authentication flows initiated                                                                             |
| AuthN pending              | Number of authentication tokens successfully generated (disregarding whether or not the client actually obtained it) |
| AuthN OK                   | Number of authentication tokens successfully obtained by users                                                       |
| AuthZ requested            | Number of attempted authorizations                                                                                   |
| AuthZ OK                   | Number of successful authorizations                                                                                  |
| AuthZ failed               | Number of denied authorizations by MVPDs at application level                                                        |
| Play request               | Number of short media tokens generated (which assimilate with the number of play requests)                           |
| Logout requested           | Number of logout flows initiated                                                                                     |
| Logout completed           | Number of logout flows completed with success                                                                        |
| Logout failed              | Number of failed logout flows                                                                                        |
| Preauthorization requested | Number of preauthorization flows initiated                                                                           |
| Preauthorization OK        | Number of successful preauthorization events with the resources that were preauthorized                              |
| Preauthorization denied    | Number of preauthorization events with the resources that were denied preauthorization                               |
| Preauthorization failed    | Number of preauthorization events that failed                                                                        |

| Adobe Analytics Name   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Channel                | The requestor ID used to perform the entitlement request                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| MVPD                   | The MVPD responsible for granting entitlement to the user                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Proxy                  | The proxy MVPD (which will be "Direct" for direct integrations)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| SDK type               | The client SDK used (Flash, HTML5, Android native, iOS, Clientless etc.)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| SDK version            | The version of the Adobe Pass authentication client SDK                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Resource ID            | The actual resource title involved in the authorization request (extracted from the MRSS payload as the item/title if provided)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| AuthZ error type       | The reason for failures, as reported by Adobe Pass authentication <br/> Here are the most common values <br/> **noAuthZ** = the MVPD replied that the user does not have the channel in their package<br/> **network** = we couldn't reach the MVPD (MVPD has an issue at the moment of the call and did not reply)<br/> **norefreshtoken** = this is strictly for OAuth implementations and it might result if the user changed their password or the MVPD denied it for some reason. It typically results in a new authentication<br/> **mismatch** = if the request is made from a device that's different than the one that had the authentication token. Can result if users try to trick the system but most of these happened in the context of our old JavaScript SDK where the device ID was using the IP address as part of the computation. If a user watched TVE at home and then at work this error would be triggered and they would have to authenticate again<br/> **invalid** = invalid request, missing or invalid parameters<br/>  **authzNone** = Programmers have the ability to deny authorizations for a specific channelxMVPD combination. This is triggered by a backend API that Programmers have access to<br/> **fraud** = it's a protection mechanism on our side. If the user fails authorization and then requests it again a number of times in a short interval (seconds) we deny the call directly. It typically happens when a Programmer has a bug in their implementation that asks for authorization constantly if it fails. |
| Token Type             | When tokens are created due to AuthZ All and AuthN All, we have to know what are made caused by a degradation measure.<br/> They are:<br/> "normal" = The normal case<br/> "authnall" = When AuthN All is enabled<br/> "authzall" = When AuthZ All is enabled<br/>  "hba" = When HBA is enabled |
| Clientless device type | The device platform (alternative), currently used for Clientless.<br/> The values can be:<br/> N/A - the event did not originate from a Clientless SDK<br/> Unknown - Since the deviceType parameter from a **Clientless API** is optional, there are calls that do not contain any value.<br/> Any other value that was sent through the **Clientless API**. For example, xbox, appletv, and roku.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| MVPD User ID           | Replaces cookie based visitor ID |

 
## Details {#details-int-authn-analyt}

* The metrics will be inserted, event by event in the specific report suite via Adobe Analytics Data Insertion API
* The insertion will be batched and sent every 30 minutes. Due to this, the report needs to be time-stamped
* Each customer will have one or multiple report suites. One requestor ID (channel) will map only to one report suite. Multiple requestor IDs can map to only one report suite.
* Historical data can be provided but special care will need to be taken due to traffic/performance concerns.
* The unique visitor variable is set to the MVPD User ID
* The mapping of events and eVars is not configurable.
 

## SLA {#sla-int-authn-serv-anal}

Since it's not a critical component there is no SLA guarantee for the integration.

## Report suite configuration {#report-suite-config}

The report must be timestamped since the events will be sent in batches.

### Events {#report-suite-config-events}
 

>[!NOTE]
>All should be set with:
>
>* Counter (no subrelationships)
 
| Event                                 | Adobe Analytics event |
|---------------------------------------|-----------------------|
| AuthN requested                       | event1                |
| AuthN pending                         | event2                |
| AuthN OK                              | event3                |
| AuthZ requested                       | event4                |
| AuthZ OK                              | event5                |
| AuthZ failed                          | event6                |
| Play request                          | event7                |
| AuthN Failed                          | event8                |
| Clientless AuthN Token Request OK     | event9                |
| Clientless AuthN Token Request Failed | event10               |
| Play request failed                   | event11               |
| Logout request                        | event12               |
| Logout completed                      | event13               |
| Logout failed                         | event14               |
| Preflight request                     | event15               |
| Preflight failed                      | event16               |
| Preflight granted                     | event17               |
| Preflight denied                      | event18               |


### eVars {#evars}
 

>[!NOTE]
>All should be set with:
>
>* Allocation: Most recent (last)
>* Expire After: Hit
>* Type: Text String
 
| Property                          | eVar                           |
|-----------------------------------|--------------------------------|
| Channel                           | eVar1                          |
| MVPD                              | eVar2                          |
| Proxy                             | eVar3                          |
| SDK type                          | eVar4                          |
| SDK version                       | eVar5                          |
| Resource ID                       | eVar6                          |
| AuthZ error type                  | eVar7                          |
| Token Type                        | eVar8                          |
| Clientless device type            | eVar9                          |
| MVPD User ID                      | visitorID (done automatically) |
| MVPD User ID                      | eVar10                         |
| Device Type                       | eVar11                         |
| Operating System                  | eVar12                         |
| Primary hardware type             | eVar13                         |
| TTL                               | eVar14                         |
| Authentication Type               | eVar15                         |
| Version of server architecture    | eVar16                         |
| External authentication provider  | eVar17                         |
| Latency                           | eVar18                         |
| Visitor Id                        | eVar19                         |
| SSO Mechanism                     | eVar20                         |
| Device Model                      | eVar21                         |
| Device Version                    | eVar22                         |
| Device Hardware Model             | eVar23                         |
| Device Hardware Vendor            | eVar24                         |
| Device Hardware Manufacturer      | eVar25                         |
| Device Hardware Version           | eVar26                         |
| Device OS Name                    | eVar27                         |
| Device OS Family                  | eVar28                         |
| Device OS Vendor                  | eVar29                         |
| Device OS Version                 | eVar30                         |
| Device Browser Name               | eVar31                         |
| Device Browser Vendor             | eVar32                         |
| Device Browser Version            | eVar33                         |
| Normalized Clientless device type | eVar34                         |

## Pricing {#pricing}

Please contact your TAM for more information.
