---
title: JavaScript SDK API Reference
description: JavaScript SDK API Reference
exl-id: 48d48327-14e6-46f3-9e80-557f161acd8a
---
# JavaScript SDK API Reference {#javascript-sdk-api-reference}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## API Reference {#api-reference}

These functions initiate requests for interaction with an MVPD. All calls are asynchronous; you must implement [callbacks](#callbacks) to handle the responses:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor (inRequestorID, endpoints, options){#setrequestor(inRequestorID,endpoints,options)}

**Description:** Identifies the site from which the requests originate.  You must make this call before any other API calls in a communication session. 

**Parameters:**

- *inRequestorID* - The unique identifier that Adobe assigned to the originating site during registration.

- *endpoints* - This parameter is optional. It can be one of the following values:

  - An array that allows you to specify endpoints for authentication and authorization services provided by Adobe(different instances might be used for debugging purposes). In case that multiple URLs are provided, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD. By default (if no value is specified), the Adobe service provider is used (<http://sp.auth.adobe.com/>).
  
  Example:
  - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`

- *options* -  A JSON object containing the Application ID value, Visitor ID value refresh-less settings (background login logout) and MVPD settings (iFrame). All values are optional.
    1.  If specified, the Experience Cloud visitorID would be reported on all network calls performed by the library. The value can be later used for advanced analytics reports.
    2.  If the unique identifier of the application is specified -`applicationId` - the value will be added to all subsequent calls made by the application as part of the X-Device-Info HTTP header. This value can be later fetched from [ESM](/help/authentication/entitlement-service-monitoring-overview.md) reports using the proper query.

  **Note:** All JSON keys are case-sensitive.

    Example:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })

```

- The Programmer can override the MVPD settings that are configured in Adobe Primetime authentication, by specifying if an iFrame is required or not for login (*iFrameRequired* key) and the iFrame dimensions (*iFrameWidth* and *iFrameHeight* keys). The JSON object has the following template:

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

All the top-level keys in the template above are optional and have default values (*backgroundLogin*, *backgroundLogut*are false by default, and mvpdConfig is null - meaning that no MVPD settings are overriden).

 
- **Note**:  Specifying invalid values / types for the above parameters will result in undefined behavior.

 

Here is an example configuration for the following scenario: activating refresh-less login and logout, changing MVPD1 to full page-redirect login (non-iFrame) and MVPD2 to iFrame login with width=500 and height=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**Callbacks triggered:** [setConfig()](#setconfigconfigxml-setconfigconfigxml) 
</br>

[Back To Top](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Description:** Requests authorization for the specified resource. Each time a customer tries to access an authorizable resource, call this function to obtain a short-lived authorization token from the Access Enabler. Resource IDs are agreed upon with the MVPD providing authorization.

Uses the cached authentication token for the current customer. If no such token is found, initiates the authentication process first, then continues with authorization.  
 
**Parameters:**

- `inResourceID` - The ID of the resource for which the user requests authorization.
- `redirect_url` -  Optionally provide a redirect URL, so that the MVPD's authorization process returns the user to that page rather than the page from which authorization was initiated.


**Callbacks triggered:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) on success, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) on failure

>[!CAUTION]
>
>Please use checkAuthorization() instead of getAuthorization() whenever possible. The getAuthorization() method will start a full authentication flow (if the user is not authenticated) and this could lead to a complicated implementation on the Programmer's side.

</b>

[Back To Top](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Description:** Requests authentication for the current customer. Typically called in response to a click on a Login button. Checks for a cached authentication token for the current customer. If no such token is found, initiates the authentication process. This invokes the default or custom provider-selection dialog, then uses the selected provider to redirect to the MVPD's login interface.

On success, creates and stores an authentication token for the user. If authentication fails, the provider returns an appropriate error message to your [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) callback.

**Parameters:**

- redirect_url - Optionally provide a redirect URL, so that the MVPD's authentication process returns the user to that page rather than the page from which authentication was initiated.

 **Callbacks triggered:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Back To Top](#top)

</br>

## checkAuthN {#checkauthn}

**Description:** Checks current authentication status for the current customer.  Not associated with any UI.

**Callbacks triggered:** [setAuthentcationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Back To Top](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Description:** This method is used by the application to check the authorization status for the current customer and the given resource. It starts by checking the authentication status first. If not authenticated, the tokenRequestFailed() callback is triggered, and the method exits. If the user is authenticated, it also triggers the authorization flow. See details on the [getAuthorization()](#getAuthZ method.

>[!TIP]
>
> **Using check-status functions**  You do not need to check the status of either authentication or authorization before requesting authorization. You can call these functions, for example, to update your own status display. Do not use them when you require any user interaction.

**Parameters:**

- `inResourceID` - The ID of the resource for which the user requests authorization.

 
**Callbacks triggered:**
  [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Description:** Requests "preflight" authorization status for a list of
resources.

**Parameters:**

- *resources*: The resources parameter is an array of resources for which the authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it is an agreed upon value established between the Programmer and the MVPD, or a media RSS fragment. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

This API variant is available starting with JS SDK version 4.0


**Parameters:**

- *resources*: The resources parameter is an array of resources for which the authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it is an agreed upon value established between the Programmer and the MVPD, or a media RSS fragment. 

- *cache*: Wether to use the internal cache when checking for preauthorized resources. This is an optional parameter, defaulting to **true**. If true the behavior is identical to the above API, meaning that subsequent calls to this function will use an internal cache to resolve preauthorized resource. Passing **false** for this parameter will disable the internal cache, resulting in a server call each time the **checkPreauthorizedResources** API is called.

**Callbacks triggered:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[Back To Top](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Description:** Retrieves information exposed as metadata by the Access Enabler library.

There are two types of metadata: 

- **Static** (Authentication token TTL, Authorization token TTL, and Device ID) 
- **User Metadata** (This includes user specific information that is passed from the MVPD to the user's device during the Authentication and/or Authorization flows)

**More Information:** [User Metadata](#UserMetadata)

**Parameters:**

- *key*: An id that specifies the requested metadata:
    - If key is `"TTL_AUTHN",` then the query is made to obtain the authentication token expiration time.
    
    - If key is `"TTL_AUTHZ"` and params is an array containing the resource id as a string, then the query is made to obtain the expiration time of the authorization token associated to the specified resource.
    
    - If key is `"DEVICEID"` then the query is made to obtain the current device id. Note that this feature is disabled by default and Programmers should contact Adobe for information regarding enablement and fees.
    
    - If key is from the following list of user metadata types, a JSON object containing the corresponding user metadata is sent to the [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) callback function:
        
    - `"zip"` - Zip Code
        
    - `"encryptedZip"` - Encrypted Zip Code
        
    - `"householdID"` - Household identifier. In the case when an MVPD does not support subaccounts this will be identical to userID.
        
    - `"maxRating"` - Maximum parental rating for the user
        
    - `"userID"` - The user identifier. In the case in which an MVPD supports subaccounts, and the user is not the main account, userID will be different than householdID.
        
    - `"channelID"` - The list of channels that  user is entitled to view
        
    - `"is_hoh"` - Flag that identifies if a user is head of household
        
    - `"encryptedZip"` - Encrypted zip code
        
    - `"typeID"` - Flag that identifies if the user account is primary/secondary account
        
    - `"primaryOID"` - Household identifier
        
    - `"postalCode"` - Similar to zip code
        
    - `"acctID"` - Account ID
        
    - `"acctParentID"` - Account Parent ID

    **Note**:  The actual User Metadata available to a Programmer depends on what an MVPD makes available.  See [User Metadata](#UserMetadata) for the current list of available User Metadata.


For example:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**Callbacks triggered:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Back To Top](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**Description:** Call this function when the user has selected an MVPD from your provider-selection UI in order to send the provider selection to the Access Enabler or call this function with a null parameter in case the user dismissed your provider-selection UI without selecting a provider. 

**Callbacks
triggered:**[setAuthentcationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Back To Top](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**Description:** Retrieves the results of the customer's selection in the provider-selection dialog. This can be used at any time after the initial authentication check.

This function is asynchronous, and returns its result to your `selectedProvider()` callback function.

- **MVPD** The currently selected MVPD, or null if no MVPD was selected.
- **AE_State** The result of authentication for the current customer one of "New User", "User Not Authenticated", or "User Authenticated"

 **Callbacks triggered:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Back To Top](#top)

</br>

## logout {#logout}

**Description:** Logs out the current customer, clearing all authentication and authorization information for that user. Deletes all authN and authZ tokens from the customer's system.

 **Callbacks triggered:** [setAuthentcationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[Back To Top](#top)

</br>

## Callback Definition {#calllback-definitions}

You must implement these callbacks to handle the responses to your asynchronous request calls:

- [entitlementLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entitlementLoaded() {#entitlementLoaded}

**Description:** Triggered when the Access Enabler has completed initialization and is ready to receive requests. Implement this callback to know when you can start the communication with the Access Enabler API.
</br>

[Back to top](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Description:** Implement this callback to receive the configuration information and MVPD list.
 
**Parameters:**

- *configXML*: xml object holding the configuration for the current REQUESTOR including the MVPD list.

 
**Triggered by:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Back to top](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**Description:** Implement this callback to invoke your own custom provider-selection UI. Your dialog should use the display name (and optional logo) to provide the customer's choices. When the customer has made a choice and dismissed the dialog, send the associated ID for the chosen provider in the call to *setSelectedProvider()*.

**Parameters:**

- *providers* - An array of Objects representing the requested MVPDs:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Triggered by:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Back to top](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Description:** Implement this callback if the user selected a MVPD which requires an iFrame in which to display its authentication login page UI.

**Triggered by:**[setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Back to top](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Description:** Implement this callback to receive the authentication status (1=authenticated or 0=not authenticated) and a descriptive error message if any error occurred while attempting to determine the authentication status (empty string on successful completion of the check).

>[!NOTE] 
> 
>If you are using the current, [Advance Error Reporting](/help/authentication/error-reporting.md) system, you can ignore the errorCode paramer sent to this function.  However, the isAuthenticated flagis still of use for tracking the authentication status of a user in the entitlement flow


**Parameters:**

- *isAuthenticated* - Provides authentication status: 1 (authenticated) or 0 (not authenticated).
- *errorCode* - Any error that occurred when determining authentication status. An empty string if none.

 
**Triggered by:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Back to top](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>The device type and operating system are derived through the use of a public Java library (<http://java.net/projects/user-agent-utils>) and the user agent string. Be advised that this information is provided only as a coarse way to break down operational metrics into device categories, but that Adobe can take no responsibility for incorrect results. Please use the new functionality accordingly.

**Description:** Implement this callback to receive tracking data when specific events occur. You can use this, for example, to keep track of how many users have logged in with the same credentials. Tracking is not currently configurable. With Adobe Primetime authentication 1.6, `sendTrackingData()` also reports information on the device, the Access Enabler client, and the operating system type. The `sendTrackingData()` callback remains backwards compatible.  
 
- Possible values for device type:
    - computer
    - tablet
    - mobile
    - gameconsole
    - unknown

- Possible values for Access Enabler client type:
    - html5
    - ios
    - android

  
Passes the event type and an array of associated information. Event types are:

| mvpdSelection           | The user selected an MVPD in a provider-selection dialog. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | An authentication check is complete.                      |
| authorizationDetection  | An authorization request is complete.                     |

</br>
Data is specific to each event type:
</br>

|Event type (String) | Data (Array)  | 
|:--- | :--- |
|mvpdSelection|0: Selected MVPD|
||1: Device Type|
||2: Access Enabler client Type|
||3: OS|
|authenticationDetection|0: Whether the token request was successful (true/false)|
||1: MVPD ID|
||2: GUID|
||3: Token already in cache (true/false)|
||4: Device Type|
||5: Access Enabler client Type|
||6: OS|
|authorizationDetection|0: Whether the token request was successful (true/false)|
||1: MVPD ID|
||2: GUID|
||3: Token already in cache (true/false)|
||4: Error|
||5: Details|
||6: Device Type|
||7: Access Enabler client Type|
||8: OS|


**Triggered by:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Back to top](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Description:** Implement this callback to receive the short-lived media token (inToken) and the ID of the resource (inRequestedResourceID)for which an authorization request or a check-authorization request was made and has completed successfully.

**Triggered by:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Back to top](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Description:** Implement this callback to be signaled when an  authorization or a check-authorization request has failed. Can optionally be used by an MVPD to provide a custom message to be  displayed by the Programmer.

>[!IMPORTANT]
>
>This callback function is part of the older, original Primetime authentication error reporting system. It is retained for backwards compatibility, but it is not necessary touse this function at all if you have implemented your own callbacks using the current, Advanced Error Reporting system. The newer error reporting system provides more detailed information about why an authorization (or other operation) failed, along with suggested courses of action for each type of error or warning.

**Parameters:**

- *inRequestedResourceID* - A string providing the Resource ID that was used on the authorization request.
- *inRequestErrorCode* - A string that displays the Adobe Primetime authentication error code, indicating the reason for the failure; possible values are "User Not Authenticated Error" and "User Not Authorized Error"; for more details, see "Callback error codes" below.
- *inRequestDetailedErrorMessage* - An additional descriptive string suitable for display. If this descriptive string is not available for any reason, Adobe Primetime authentication sends an empty string **("")**.  This can be used by an MVPD to pass custom error messages or sales-related messages. For example, if a subscriber is denied authorization for a resource, the MVPD could reply with an `*inRequestDetailedErrorMessage*` such as: **"You currently do nothave access to this channel in your package. If you would like to upgrade your package click \*here\*."** The message is passed by Adobe Primetime authentication through this callback to the Programmer's site. The Programmer then has the option to display or ignore it. Adobe Primetime authentication can also use `*inRequestDetailedErrorMessage*` to notify the Programmer of the condition that might have led to an error. For example, **"A network error occurred when communicating with the provider's authorization service".**

 

**Triggered by:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Back to top](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Description:** Callback triggered by the Access Enabler that delivers the authorized resources list returned after a call to `checkPreauthorizedResources()`.

**Parameters:**

- *authorizedResources*: The list of authorized resources.

**Triggered by:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Back to top](#top)

</br>

## setMetadataStatus(key, encrypted, data) {#setMetadataStatus(key,encrypted,data)}

**Description:** Callback triggered by the Access Enabler that delivers the metadata requested via a `getMetadata()` call.

**More Information:** [User Metadata](#userMetadata)

**Parameters:**

- *key (String)*: The key of the metadata for which the request was made.
- *encrypted (Boolean)*: A flag signifying whether the "value" is encrypted or not. If this is "true" then "value" will actually be a JSON Web Encrypted  representation of the actual value. 
- *data (JSON Object)*: A JSON Object with the representation of the metadata.For simple requests ('`TTL_AUTHN`', '`TTL_AUTHZ`', '`DEVICEID`'), result is a String (representing the Authentication TTL, Authorization TTL or Device ID). In case of a User Metadata request, result can be a primitive or JSON object representing the metadata payload. The actual structure of JSON user metadata objects is similar to the following:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

For example:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**Triggered by:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Back to top](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**Description:** Implement this callback to receive the currently selected MVPD and the result of authentication of current user wrapped up in the `result` parameter. The `result` parameter is an Object with the following properties:

- **MVPD** The currently selected MVPD, or null if no MVPD was selected.
- **AE\_State** The result of authentication for the current user, one of "New User", "User Not Authenticated", or "User Authenticated

 **Triggered by:** [getSelectedProvider()](#getSelProv)

</br>

[Back to top](#top)

</br>

### Callback Error Codes {#callback-error-codes}

|Generic Errors | | 
|:--- | :--- | 
|Internal Error | A system error occurred when trying to process request.|
|Provider not Selected Error| Occurs when customer cancels in the provider selection dialog|
|Provider not Available Error|  Occurs when no providers are available.| 

|Authentication Errors | | 
|:--- | :--- | 
|Generic Authentication Error | Returned when the reason is not known or cannot be published. |
|Internal Authentication Error | A system error occurred when trying to authenticate. | 
| User Not Authenticated Error | User is not authenticated. | 
| Multiple Authentication Requests Error | Additional authentication requests were received before the first one completed. |

|Authorization Errors | |
|:--- | :--- | 
|Generic Authorization Error | Returned when the reason is not known or cannot be published.| 
|Internal Authorization Error |   A system error occurred when trying to authorize. |
|User not Authorized Error |  The customer is not authorized to view the requested content. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[Back To Top](#top)
