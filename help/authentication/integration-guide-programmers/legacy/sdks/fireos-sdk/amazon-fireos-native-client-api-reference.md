---
title: Amazon FireOS Native Client API Reference
description: Amazon FireOS Native Client API Reference
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
---
# (Legacy) Amazon FireOS Native Client API Reference {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#intro}

This document details the methods and callbacks exposed by the Amazon FireOS SDK for Adobe Pass Authentication, supported with Adobe Pass Authentication. The methods and callback functions described here are defined in the AccessEnabler.h and EntitlementDelegate.h header files.

Please refer to <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> for the latest Amazon FireOS AccessEnabler SDK. 

>[!NOTE]
>
>The Adobe Pass Authentication team encourages you to use only Adobe Pass Authentication *public* APIs:

- Public APIs are available *and fully tested* on all supported client types. For any public feature, we make sure that each client type has a corresponding version of the associated method(s).
- Public APIs are required to be as stable as possible, to support backwards compatibility and ensure that partner integrations do not break. However, for *non*-public APIs, we reserve the right to change their signature at any future point. If you encounter a particular flow that cannot be supported through a combination of the current public Adobe Pass Authentication API calls, the best approach is to let us know. Taking into account your needs, we can modify the public APIs and provide a stable solution moving forward.

## Amazon FireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [logout](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**Description:** Instantiates the Access Enabler object. There should be a single Access Enabler instance per application instance.

| API call: constructor |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br>    
```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**Availability:** v3.0+


**Parameters:**

- *appContext*: Amazon Fire OS application context.
- softwareStatement
- redirectUrl : in case of FireOS, the parameter value will be ignored and set to default : adobepass://android.app
- env_url: for testing using Adobe staging environment, env\_url can be set to "sp.auth-staging.adobe.com"

**Deprecated:**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**Description:** Establishes the identity of the Programmer. Each Programmer is assigned a unique ID upon registering with Adobe for the Adobe Pass Authentication system. This setting should be performed only once during the application's life cycle.

The server response contains a list of MVPDs together with some configuration information that is attached to the identity of the Programmer. The server response is used internally by the Access Enabler code. Only the status of the operation (i.e. SUCCESS/FAIL) is presented to your application via the setRequestorComplete() callback.

If the *urls* parameter is not used, the resulting network call targets the default service provider URL: the Adobe Release/Production environment.  

If a value is provided for the *urls* parameter, the resulting network call targets all the URLs provided in the *urls* parameter. All configuration requests are triggered simultaneously in separate threads. The first responder takes precedence when compiling the list of MVPDs. For each MVPD in the list, the Access Enabler remembers the URL of the associated service provider. All subsequent entitlement requests are directed to the URL associated with the service provider that was paired with the target MVPD during the configuration phase.

| API call: requestor configuration |
| --- |
| ```public void setRequestor(String requestorId)``` |


**Availability:** v3.0+


| API call: requestor configuration |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Availability:** v3.0+


**Parameters:**

- *requestorID*: The unique ID associated with the Programmer. Pass the unique ID assigned by Adobe to your site when you first registered with the Adobe Pass Authentication service.
- *urls*: Optional parameter; by default, the Adobe service provider is used (http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass Authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.

**Callbacks triggered:** `setRequestorComplete()`

 

**Deprecated:**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**Description:** Callback triggered by the Access Enabler that informs your application that the configuration phase is complete. This is a signal that the app can start issuing entitlement requests. No entitlement requests can be issued by the application until the configuration phase is complete.

| Callback: requestor configuration complete |
| --- |
| ```public void setRequestorComplete(int status)``` |

**Availability:** v1.0+

**Parameters:**

- *status*: Can take one of the following values:
    - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - configuration
      phase was successfully completed
    - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - configuration
      phase failed

**Triggered by:** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**Description:** Configures global SDK options. It accepts a **Map\<String, String\>** as an argument. The values from the map will be passed to the server along with every network call that the SDK makes.

The values will be passed to the server independent of the current flow (authentication/authorization). If you want to change the values you can call this method at any point in time.

 

| API call: setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**Availability:** v3.0+

**Parameters:**

- *options*: A Map\<String, String\> containing global SDK options. Currently the following options are available:
    - **applicationProfile** - It can be used to make server configurations based on this value.
    - **ap\_vi** - The Experience Cloud ID Service. This value can be later used for advanced analytics reports.
    - **device\_info** - Device Information as described in **Passing device information cookbook**

</br>

### checkAuthentication {#checkAuthN}

**Description:** Checks the authentication status. It does this by searching for a valid authentication token in the local token storage space. Calling this method performs no network calls. It is used by the application to query the user's authentication status and update the UI accordingly (i.e. update the login / logout UI). The authentication status is communicated to the application via the [*setAuthenticationStatus()*](#setAuthNStatus) callback.

If an MVPD supports the "Authentication per Requestor" feature, then multiple authentication tokens can be stored on a device. 

| API call: check authentication status |
| --- |
| ```public void checkAuthentication()``` |

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** `setAuthenticationStatus()`  

</br>

### getAuthentication {#getAuthN}

**Description:** Starts the full authentication workflow. It starts by checking the authentication status. If not already authenticated, the authentication flow state-machine is started:

- If the last authentication attempt was successful, the MVPD selection phase is skipped and a WebView control will presents the user with the MVPD's login page.
- If the last authentication attempt was unsuccessful or if the user explicitly logged out, the [*displayProviderDialog()*](#displayProviderDialog) callback is triggered. Your application uses this callback to display the MVPD selection UI. Also your app is required to resume the authentication flow by informing the Access Enabler library about the user's MVPD selection via the [setSelectedProvider()](#setSelectedProvider) method.

If an MVPD supports the "Authentication per Requestor" feature, then multiple authentication tokens can be stored on a device (one per Programmer).

Finally, the authentication status is communicated to the application via the *setAuthenticationStatus()* callback.

| API call: initiates the authentication flow |
| --- |
| ```public void getAuthentication()``` |

**Availability:** v1.0+

| API call: initiates the authentication flow |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**Availability:** v1.0+

**Parameters:**

- *forceAuthn*: A flag that specifies if the authentication flow should be started, regardless if the user is already authenticated or not.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK.

**Callbacks triggered:** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**Description** Callback triggered triggered by the Access Enabler to inform the application that the appropriate UI elements need to be instantiated to allow the user to select the desired MVPD. The callback provides a list of MVPD objects with additional information that can help to correctly build the selection UI panel (such as the URL pointing to the MVPD's logo, friendly display name, etc.)
  
Once the user has selected the desired MVPD, the upper-layer application is required to resume the authentication flow by calling *setSelectedProvider()* and passing it the ID of the MVPD corresponding to the user's selection.  
 

| **Callback: display the MVPD selection UI** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**Availability:** v1.0+

**Parameters**:

- *mvpds*: List of MVPD objects holding MVPD-related information that the application can use to build the MVPD selection UI elements.

**Triggered by:** `getAuthentication(), getAuthorization()`  

</br>

### setSelectedProvider {#setSelectedProvider}

**Description:** This method is called by your application to inform the Access Enabler of the user's MVPD selection. When passing *null* as a parameter, the Access Enabler reset the current MVPD to a null value.

| **API call: set the currently selected provider** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**Availability:**v 1.0+

**Parameters:** None
  
**Callbacks triggered:** `setAuthenticationStatus(), sendTrackingData()` 
</br>

### navigateToUrl {#navigagteToUrl}

**Description:** Callback triggered by the Access Enabler on Android SDK. It should be ignored on Amazon FireOS SDK.

| **Callback: display MVPD login page** |
| --- |
| ```public void navigateToUrl(String url)``` |

**Availability:** v1.0+

**Parameters:**

- *url*: The URL pointing to the MVPD's login page

**Triggered by:** `getAuthentication(), setSelectedProvider()`  

</br>

### getAuthenticationToken {#getAuthNToken}

**Description:** Completes the authentication flow by requesting the authentication token from the back-end server. 

| **API call: retrieve the authentication token** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**Availability:** v1.0+

**Parameters:**

- *cookies*: Cookies that are set on the the target domain (see the demo application in the SDK for a reference implementation).
  
**Callbacks triggered:** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**Description:** Callback triggered by the Access Enabler which informs the application of the status of the authentication. There are many places where authentication flow can fail, either as a result of user's interaction or due to other unforeseen scenarios (i.e. network connectivity problems, etc.). This callback informs the application of the success/failure status of the authentication, while also providing additional information about the failure reason, when needed.

This callback also signals when the logout flow is complete.

| **Callback: report the status of the authentication flow** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**Availability:** v1.0+

**Parameters:**

- *status*: Can take one of the following values:
    - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - authentication flow was successfully completed
    - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - authentication flow failed
    - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT` - logout
- *code*: Reason for presented status. If *status* is `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`, then *code* is an empty string (i.e., defined by the `AccessEnabler.USER_AUTHENTICATED` constant). If not authenticated, this parameter can take one of the following values:
    - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR` - The user is not authenticated. In response to the *checkAuthentication()* method call when there is no valid authentication token in the local token cache.
    - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - The AccessEnabler has reset the authentication state-machine after the upper-layer application passed *null* to `setSelectedProvider()` to abort the authentication flow.  Presumably the user has canceled the authentication flow (i.e., pressed the "Back" button).
    - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR` - The authentication flow failed due to reasons such as network unavailability or the user canceled the authentication flow explicitly.
    - `AccessEnabler.LOGOUT` - The user is not authencated due to a logout action. 

**Triggered by:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**Description:** This method is used by the application to determine if the user is already authorized to view specific protected resources. The primary purpose of this method is to retrieve information for use in decorating the UI (for example, indicating access status with lock and unlock icons).

| **API call: set the currently selected provider** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Availability:** v1.0+

**<Parameters:** The `resources` parameter is an array of resources for which authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it should be an agreed upon value established between the Programmer and the MVPD or a media RSS fragment.

**Callback triggered:** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**Description:** Callback triggered by checkPreauthorizedResources(). Provides a list of resources the user is already authorized to view.

| **API call: set the currently selected provider** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Availability:**v 1.0+

**Parameters:** The `resources` parameter is an array of resources for which the user is already authorized to view.

**Triggered by:** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**Description:** This method is used by the application to check the authorization status. It starts by checking the authentication status first. If not authenticated, the *setTokenRequestFailed()* callback is triggered, and the method exits. If the user is authenticated, it also triggers the authorization flow. See details on the *getAuthorization()* method.

| **API call: check authorization status** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**Availability:** v1.0+

| **API call: check authorization status** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Availability:** v1.0+

**Parameters:**

- *resourceId*: The ID of the resource for which the user requests authorization.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK.
  
**Callbacks triggered:** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`  

</br>

### getAuthorization {#getAuthZ}

**Description:** This method is used by the application to initiate the authorization flow. If the user is not already authenticated, it also initiates the authentication flow. If the user gets authenticated, the Access Enabler proceeds to issue requests for the authorization token (if no valid authorization token is present in the local token cache) and for the short-lived media token. Once the short media token is obtained, the authorization flow is considered complete. The *setToken()* callback gets triggered and the short media token is delivered as a parameter to the application. If for any reason, the authorization fails, the *tokenRequestFailed()* callback is triggered and the error code and details are provided.

| **API call: initiate the authorization flow** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**Availability:** v1.0+

| **API call: initiate the authorization flow** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Availability:** v1.0+

**Parameters:**

- *resourceId*: The ID of the resource for which the user requests authorization.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 
  
**Callbacks triggered:** `tokenRequestFailed(), setToken(), sendTrackingData()`  

|     |     |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **Additional callbacks triggered**  <br>This method can also trigger the following callbacks (if the authentication flow is also initiated): _setAuthenticationStatus()_, _displayProviderDialog()_ |

**NOTE: Please use checkAuthorization() instead of getAuthorization() whenever possible. The getAuthorization() method will start a full authentication flow (if the user is not authenticated) and this could lead to a complicated implementation on the Programmer's side.**

</br>

### setToken {#setToken}

**Description:** Callback triggered by the Access Enabler that informs your application that the authorization flow was completed successfully. The short-lived media token is also delivered as a parameter.

| **Callback: authorization flow completed successfully** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**Availability:**v 1.0+

**Parameters:**

- *token*: The short-lived media token
- *resourceId*: The resource for which the authorization was obtained

**Triggered by:** `checkAuthorization(), getAuthorization()`  

<br>

### tokenRequestFailed {#tokenRequestFailed}

**Description:** Callback triggered by the Access Enabler that informs the upper-layer application that the authorization flow failed.

| **Callback: authorization flow failed** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**Availability:** v1.0+

**Parameters:**

- *resourceId*: The resource for which the authorization was obtained
- *errorCode*: Error code associated to the failure scenario. Possible values:
    - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR` - The user was not able to authorize for the given resource
- *errorDescription*: Additional details about the failure scenario. If this descriptive string is not available for any reason, Adobe Pass Authentication sends an empty string >**("")**.  This string can be used by an MVPD to pass custom error messages or sales-related messages. For example, if a subscriber is denied authorization for a resource, the MVPD could send a message such as: "You currently do not have access to this channel in your package. If you would like to upgrade your package click here." The message is passed by Adobe Pass Authentication through this callback to the Programmer, who has the option to display or ignore it. Adobe Pass Authentication can also use this parameter to provide notification of the condition that might have led to an error. For example, "A network error occurred when communicating with the provider's authorization service."

**Triggered by:** `checkAuthorization(), getAuthorization()`

</br>

### logout {#logout}

**Description:** Use this method to initiate the logout flow. The logout is the result of a series of HTTP-redirect operations due to the fact that the user needs to be logged out from both Adobe Pass Authentication servers and also from the MVPD's servers. 

| **API call: initiate the logout flow** |
| --- |
| ```public void logout()``` |

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** None

</br>

### getSelectedProvider {#getSelectedProvider}

**Description:** Use this method to determine the currently selected provider.

| **API call: determine the currently selected MVPD** |
| --- |
| ```public void getSelectedProvider()``` |

**Availability:** v1.0+

**Parameters:** None
  
**Callbacks triggered:** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**Description:** Callback triggered by the Access Enabler that delivers information about the currently selected MVPD to the application.

| **Callback: information about the currently selected MVPD** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**Availability:** v1.0+

**Parameters:**

- *mvpd*: Object containing information about the currently selected MVPD

**Triggered by:** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**Description:** Use this method to retrieve information exposed as metadata by the Access Enabler library. The application can access this information by providing a composite MetadataKey object.

| **API call: query the AccessEnabler for metadata** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**Availability:** v1.0+

There are two types of metadata available to Programmers:

- Static metadata (Authentication token TTL, Authorization token TTL and Device ID) 
- User metadata (User-specific information, such as User ID and Zip Code; passed from an MVPD to a user's device during the Authentication and / or Authorization flows)

**Parameters:**

- *metadataKey*: A data structure that encapsulates a key and args variable, with the following meaning:
    - If key is `METADATA_KEY_TTL_AUTHN` then the query is made to obtain the authentication token expiration time.
    - If key is `METADATA_KEY_TTL_AUTHZ` and args contains a SerializableNameValuePair object with name = `METADATA_ARG_RESOURCE_ID` and value = `[resource_id]`, then the query is made to obtain the expiration time of the authorization token associated to the specified resource.
    - If key is `METADATA_KEY_DEVICE_ID` then the query is made to obtain the current device id. Note that this feature is disabled by default and Programmers should contact Adobe for information regarding enablement and fees.
    - If key is `METADATA_KEY_USER_META` and args contains a SerializableNameValuePair object with name = `METADATA_KEY_USER_META` and value = `[metadata_name]`, then the query is made for user metadata. The current list of available user metadata types:
        - `zip` - Zip Code
        - `householdID` - Household identifier. If an MVPD does not support subaccounts, this will be identical to `userID`.
        - `maxRating` - Maximum parental rating for the user
        - `userID` - The user identifier. If an MVPD supports subaccounts, and the user is not the main account, 
        - `channelID` - A list of channels the user is entitled to view

The actual User Metadata available to a Programmer depends on what an MVPD makes available.  This list will be further expanded as new metadata is made available and added into the Adobe Pass Authentication system.

**Callbacks triggered:** [`setMetadataStatus()`](#setMetadaStatus)

**More Information:** [User Metadata](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**Description:** Callback triggered by the Access Enabler that delivers the metadata requested via a *getMetadata()* call.

| **Callback: result of metadata retrieval request** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Availability:** v1.0+

**Parameters:**

- *key*: The MetadataKey object containing the key for which metadata value is requested and associated parameters (see demo application for a reference implementation).
- *result*: A composite object containing the requested metadata. The object has the following fields:
    - *simpleResult*: a String that represents the metadata value when the request was made for Authentication TTL, Authorization TTL, or Device ID. This value is null if the request was made for User Metadata.
  
    - *userMetadataResult*: an Object that contains the Java representation of a JSON User Metadata payload. For example:

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      is translated into Java as: 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **The actual structure of user metadata objects is similar to the following:**

      ```json
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
 

This value is null when the request was made for simple metadata (Authentication TTL, Authorization TTL, or Device ID).

- *encrypted*: Boolean value that specifies whether the retrieved metadata is encrypted or not. This parameter is significant only for User Metadata requests, it has no meaning for Static Metadata (e.g., Authentication TTL) that is always received unencrypted. If this parameter is set to True, then it's up to the Programmer to obtain the unencrypted User Metadata value by performing an RSA decryption using the whitelisting private key (the same private key that is used for the signing of the requestor id in the [`setRequestor`](#setRequestor) call).

**Triggered by:** [`getMetadata()`](#getMetadata)

**More Information:** [User Metadata](/help/authentication/integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md)

</br>

## getVersion {#getVersion}

**Description:** Use this method to retrieve AccessEnabler current version  

| **API call: get AccessEnabler version** |
| --- |
| ```public static String getVersion()``` |

## Tracking Events {#tracking}

The Access Enabler triggers an additional callback that is not necessarily related to the entitlement flows. Implementing the event-tracking callback function named *sendTrackingData()* is optional, but it enables the application to track specific events and compile statistics such as number of successful/failed authentication/authorization attempts. Below is the specification for the *sendTrackingData()* callback:  

### sendTrackingData {#sendTrackingData}

**Description:** Callback triggered by the Access Enabler signaling to the application the occurrence of various events such as the completion/failure of authentication/authorization flows. The device type, Access Enabler client type, and operating system are also reported by sendTrackingData().

>[!WARNING]
>
> The device type and operating system are derived through the use of a public Java library (http://java.net/projects/user-agent-utils) and the user agent string. Be advised that this information is provided only as a coarse way to break down operational metrics into device categories, but that Adobe can take no responsibility for incorrect results. Please use the new functionality accordingly.

- Possible values for device type:
    - `computer`
    - `tablet`
    - `mobile`
    - `gameconsole`
    - `unknown`

- Possible values for Access Enabler client type:
    - `flash`
    - `html5`
    - `ios`
    - `tvos`
    - `android`
    - `firetv`

| Callback: tracking events |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**Availability:** v1.0+

**Parameters:**

- *event*: the event that is being tracked. There are three possible tracking events types:
    - **authorizationDetection:** any time an authorization token request returns (event type is `EVENT_AUTHZ_DETECTION`)
    - **authenticationDetection:** any time an authentication check occurs (event type is `EVENT_AUTHN_DETECTION`)
    - **mvpdSelection:** when the user selects an MVPD in the MVPD selection form (event type is `EVENT_MVPD_SELECTION`)
- *data*: additional data that is associated to the reported event. This data is presented in the form of a list of values.

Following are instructions for interpreting the values in the *data* array:

- For event type *`EVENT_AUTHN_DETECTION`:*
    - **0** - Whether the token request was successful (true/false) and if the above is true:
    - **1** - MVPD ID string
    - **2** - GUID (md5 hashed)
    - **3** - Token already in cache (true/false)
    - **4** - Device type
    - **5** - Access Enabler client type
    - **6** - Operating system type

- For event type `EVENT_AUTHZ_DETECTION`
    - **0** - Whether the token request was successful (true/false) and if successful:
    - **1** - MVPD ID
    - **2** - GUID (md5 hashed)
    - **3** - Token already in cache (true/false)
    - **4** - Error
    - **5** - Details
    - **6** - Device type
    - **7** - Access Enabler client type
    - **8** - Operating system type

- For event type `EVENT_MVPD_SELECTION`
    - **0** - ID of the currently selected MVPD
    - **1** - Device type
    - **2** - Access Enabler client type
    - **3** - Operating system type

**Triggered by:** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
