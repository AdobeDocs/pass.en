---
title: Preflight Authorization
description: Preflight Authorization
exl-id: 036b1a8e-f2dc-4e9a-9eeb-0787e40c00d9
---
# Preflight Authorization {#preflight-authorization}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Overview {#overview}

This feature provides a lightweight authorization check for multiple resources. The purpose for this lightweight check is to decorate the UI (for example, indicating access status with lock and unlock icons). Preflight authorization is as light and efficient as possible, such that a single API call yields the authorization status for a list of resources. Note that this feature is not authoritative in regards to authorizing a resource.

A `getAuthorization(resource)` or `checkAuthorization(resource)` call still MUST be made before allowing playback.

Preflight authorization also provides support for a different use case, in which the Programmer needs to request authorization for multiple resource IDs in order to allow playback of one item of media content. The Programmer can do an initial preflight check on the required resources, and depending on the response, could fail early if business conditions are not met.

For a list of MVPDs that support preflight authorization, see the [MVPD Preflight Authorization](/help/authentication/integration-guide-mvpds/mvpd-preflight-authz.md#preflight_support_list) page. 

>[!NOTE]
>
> Please note that usage of this feature for the MVPDs that don't have full preflight authorization support needs to be agreed upfront with Adobe & MVPDs. The usage of preflight authorization on these MVPDs will fall into the "worst case scenario" described [here](/help/authentication/integration-guide-mvpds/mvpd-preflight-authz.md#intro) and can lead to performance issues and slow response time. </br>
> Also, please note that usage of preflight authorization with **more than 5 resources needs to be explicitly agreed to by Adobe**.

## AccessEnabler Preflight API {#AE_pre_api}

The AccessEnabler exposes an API / callback function pair to implement preflight authorization. The API call takes a single parameter consisting of a list of resources. The callback function takes a single parameter that represents the actual authorized resources. The following examples are in ActionScript, but the calls are available in all flavors of the AccessEnabler.

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

Call this function on the AccessEnabler object to request authorization status for a list of resources.

The resources parameter is the list of resources for which the authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it is agreed upon value established between the Programmer and the MVPD, or a media RSS fragment. Note that Adobe Pass Authentication does not manage resources in any way, except for a thin mediation layer that can transform resource formats depending on what the MVPD actually supports.

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

This is a callback function that must be implemented in the Programmer's upper-layer application. The AccessEnabler will call this function after computing the authorized resources list.


### JS Example

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## Implementation Information {#details}

- [Preflight Using ChannelID](#preflight_using_channelID)
- [POST / Preauthorize](#post)
- [Storage](#storage)

The API call tries to find a cached list of authorized resources for the current user in the client's local storage. If there is no cached list, an HTTPS call is made to the AdobePass servers to retrieve the list.

The caching mechanism improves performance times on subsequent calls by skipping the network call altogether. Also, the cached list can be populated in advance as part of the authentication process.  (For information on setting up this scenario, see [Preflight Authorization Integration](/help/authentication/integration-guide-mvpds/authz-usecase.md#preflight_authz_int) in the Authorization section of the MVPD Integration Guide).

In addition, the cached list of resources can potentially be used to optimize the authorization flow, in the sense that if a cached list of resources exists, `checkAuthorization()` can check it before doing a network call. If the resource is not in the list of preauthorized resources, the check can fail without needing to call the Adobe Pass Authentication servers.


### Preflight Using ChannelID {#preflight_using_channelID}

Beginning with the Adobe Pass Authentication 2.4.1 Release, the Preflight flow works as follows:

1.  During authentication, Adobe Pass Authentication reads the `channelIID` element from the MVPD's SAML response, and uses this value to set the `authorizedResources` element in the authentication token.
1.  Inside the `checkPreauthorizedResources()` API function, Adobe Pass Authentication checks if the `authorizedResources` element is set.
1.  If the `authorizedResources` element is set, Adobe Pass Authentication reads that value and performs an intersect between the resource list from the `authorizedResources` element and the list of resources received from `checkPreauthorizedResources()` parameter.  The result of this intersection is the final list of preauthorized resources.
1.  If the `authorizedResources` element is not set, execute the previously-implemented flow, in which the list of resources received from `checkPreauthorizedResources()` parameter is passed to the PreAuthorizationServlet. This servlet performs the authorization calls to the MVPD endpoints and returns the list of preauthorized resources.

### Example of Preflight With ChannelID

The example below shows a sample channel lineup. Please note that the name of the attribute used to send the list of channels can differ from one MVPD to another:

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

The `authorizedResources` element from the authentication element appears as follows:

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

The programmer executes the `checkPreauthorizedResources()` API call, passing the following list of parameters:</span>

- "MSNBC" 
- "FBN" 
- "TruTV"
- "fbc-fox"

The current Preflight implementation performs the intersection with the list of resources from the `authorizedResources` element and returns this list:

- "MSNBC"
- "FBN"
- "TruTV"

 

**Note:** Please notice that the intersection is case insensitive.

 

### POST / Preauthorize {#post}

This call will be performed automatically by the AccessEnabler when no cached, authorized, resource list exists. 


#### Request {#req}

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `authentication_token` | string | YES | The authentication token. |
| `resource_id` | string | YES | A single resource. This can be specified multiple times, one time for each element of the resources array supplied in the `checkPreauthorizedResources()` API call. |


**Note:** The maximum number of requested resources is configurable.
**Maximum default value is 5.**


#### Response {#resp}

The response that the preauthorize servlet sends back has the following format:

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### Storage {#storage}

A list of preauthorized resources that the AccessEnabler gets from the Service Provider. This list of resources:

- Is stored along with the AuthN and the AuthZ tokens
- Is valid as long as the user is on the same website, or until the
  AuthN token expires
- Is re-retrieved each time the user lands on a new Adobe Pass
  authentication integrated website

Each entry contains the resource ID that user is preauthorized for.

For example:


| Resource ID | Authorized |
| ----------- | ---------- |
| CNN         | true       |
| TNT         | false      |
| ...         | ...        |


This list is named "preauthorization cache".

#### Flow {#flow}

1.  Programmer's app / site makes a `checkPreauthorizedResources(resourceList)` call.
1.  AccessEnabler verifies the authentication token for authorized resources:
    1.  If the authentication token contains authorized resources - this list is authoritative and no call should be made in order to get this information. Resources from resourceList are searched within the list of authorized resources on the authentication token and only those that were found are returned by the `preauthorizedResources()` callback.
    1.  If the authentication token DOES NOT contain authorized resources - `resourceList` is compared to the list of resources in the preauthorization cache.
        1.  If the list contains the same resources - this means that a call to the server was already made and the response is already in the preauthorization cache. Only resources that are authorized will be returned by the `preauthorizedResources()` callback.
        1.  If the list DOES NOT contain the same resources - the client needs to make a call to the server in order to obtain the authorization state for the resources in resourceList. The response will be fetched and stored in the preauthorization cache, completely replacing the old resources. Only resources that are authorized will be returned by the `preauthorizedResources()` callback.


#### List Retrieval {#listRetrieve}

Whenever a `checkPreauthorizedResources()` is called, the list of resources to verify for authorization is checked against the preauthorization cache. If the list contains the same set of resources, no call to the Service Provider is made, since all of the resources needed for triggering the `preauthorizedResources()` callback are already in the cache.


#### logout() {#logout}

The preauthorization cache is emptied on logout.


## Dependencies {#depends}

The performance of the Preflight API is dependent on specific MVPD implementations.  For implementation options, see [Preflight Authorization Integration](/help/authentication/integration-guide-mvpds/authz-usecase.md#preflight_authz_int) in the Authorization section of the MVPD Integration Guide.


## Security {#security}

The Client APIs are available to all Programmers.

The implementation uses HTTPS as a transport, but in order to have a lighter call, no additional security measures are employed (no signing, no FAXS).

**Attention:** Do NOT use this API in an authoritative way to determine whether a user should be granted access to a protected resource. The purpose of this API is UI decoration and / or preflighting business decisions. The `getAuthorization()` and `checkAuthorization()` calls should always be made prior to allowing playback.


## Compatibility {#compat}

This feature is supported in all flavors of the AccessEnabler: AS, JS, AIR, iOS, Android, Xbox (in 2nd-screen AuthN flow).

Preflight authorization does not support pre-authorizing resources that contain CDATA sections. The focus of the current preflight system is to support channel level filtering. Resources with CDATA sections are likely asset-level resources. Preflight does support simple `mrss` resources for channel-level pre-authorization, as long as they do not contain CDATA. 

## Integration With Other Features {#integ_w_other_features}

A possible optimization can occur on the authorization flow in order to fail fast if the resource is not in the list of preauthorized resources.

In this optimization, the server preflight endpoint integrates with the Degradation mechanism.  

If an "AuthN All" rule is in place for the MVPD and Requestor, the preflight endpoint will simply mirror back all of the resources received in the request.

The same is true if "AuthZ All" is enabled for at least one of the resources present in the request.

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
