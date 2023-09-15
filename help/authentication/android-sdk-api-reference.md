---
title: Android SDK API Reference
description: Android SDK API Reference
exl-id: f932e9a1-2dbe-4e35-bd60-a4737407942d
---
# Android SDK API Reference {#android-sdk-api-reference}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

This document details the methods and callbacks exposed by the Android SDK for Adobe Pass authentication, supported with Adobe Pass authentication versions 1.7 and later. The methods and callback functions described here are defined in the AccessEnabler.h and EntitlementDelegate.h header files.

Please refer to [https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library) for the latest Android AccessEnabler SDK. 


  **Note:** The Adobe Pass authentication team encourages you to use only Adobe Pass authentication *public* APIs:

- Public APIs are available *and fully tested* on all supported client types. For any public feature, we make sure that each client type has a corresponding version of the associated method(s).</span>
- Public APIs are required to be as stable as possible, to support backwards compatibility and ensure that partner integrations do not break. However, for *non*-public APIs, we reserve the right to change their signature at any future point. If you encounter a particular flow that cannot be supported through a combination of the current public Adobe Pass authentication API calls, the best approach is to let us know. Taking into account your needs, we can modify the public APIs and provide a stable solution moving forward.

## Android API {#api}

- [getInstance](#getInstance)
- [setOptions](#setOptions)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- preauthorize
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

### Factory.getInstance {#getInstance}

**Description:** Instantiates the Access Enabler object. There should be a single Access Enabler instance per application instance.

| API call: constructor |
| --- |
| **public static** AccessEnabler **getInstance**(Context appContext, String softwareStatement, String redirectUrl)<br>        **throws** AccessEnablerException<br><br>**public static** AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl)<br>**throws** AccessEnablerException |

**Availability:** v3.1.2+

**Parameters:**

- *appContext*: Android application context.
- env\_url: for testing using Adobe staging environment, env\_url can be set to "sp.auth-staging.adobe.com"

**Deprecated:**

```
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```



### setRequestor {#setRequestor}

**Description:** Establishes the identity of the Programmer. Each Programmer is assigned a unique ID upon registering with Adobe for the Adobe Pass authentication system. When dealing with SSO and remote tokens the authentication state can change when the application is in the background, setRequestor can be called again when the application is brought into foreground in order to synchronize with the system state (fetch a remote token if SSO is enabled or delete the local token if a logout happened in the meantime).

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

- *requestorID*: The unique ID associated with the Programmer. Pass the unique ID assigned by Adobe to your site when you first registered with the Adobe Pass authentication service.

- *signedRequestorID*: A copy of the requestor ID that is digitally signed with your private key. <!--For more details. see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

- *urls*: Optional parameter; by default, the Adobe service provider is used (http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.

**Callbacks triggered:** `setRequestorComplete()`

Deprecated:

    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor (String requestorId, String signedRequestorId, ArrayList<String> urls)

[Back to Android API...](#api)

### setRequestorComplete {#setRequestorComplete}

**Description:** Callback triggered by the Access Enabler that informs your application that the configuration phase is complete. This is a signal that the app can start issuing entitlement requests. No entitlement requests can be issued by the application until the configuration phase is complete.

| Callback: requestor configuration complete |
| --- |
| java public void setRequestorComplete(int status) |

**Availability:** v1.0+

**Parameters:**

- *status*: Can take one of the following values:
    - SDK \>= 3.4.0
        - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS` - configuration phase was successfully completed
        - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR` - configuration phase failed
    - SDK \< 3.4
        - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - configuration phase was successfully completed
        - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - configuration phase failed

**Triggered by:** `setRequestor()`

[Back to Android API...](#api)

### setOptions {#setOptions}

**Description:** Configures global SDK options. It accepts a **Map\<String, String\>** as an argument. The values from the map will be passed to the server along with every network call that the SDK makes.

The values will be passed to the server independent of the current flow (authentication/authorization). If you want to change the values you can call this method at any point in time.

| API call: setOptions |
| --- |
| public void setOptions(HashMap<String,String> options) |

**Availability:** v1.9.2+

**Parameters:**

- *options*: A Map<String, String> containing global SDK options. Currently, the following options are available:
  - **applicationProfile** - It can be used to make server configurations based on this value.
  - **ap_vi** - The Marketing Cloud visitorID. This value can be later used for advanced analytics reports.
  - **ap_ai** - The Advertising ID
  - **device_info** - Client information as described here: [Passing client information device connection and application](/help/authentication/passing-client-information-device-connection-and-application.md).

[Back to top...](#apis)


### checkAuthentication {#checkAuthN}

**Description:** Checks the authentication status. It does this by searching for a valid authentication token in the local token storage space. Calling this method performs no network calls. It is used by the application to query the user's authentication status and update the UI accordingly (i.e. update the login / logout UI). The authentication status is communicated to the application via the [*setAuthenticationStatus()*](#setAuthNStatus) callback.

If an MVPD supports the "Authentication per Requestor" feature, then multiple authentication tokens can be stored on a device.  For details on this feature, see the [Caching Guidelines](#$caching) section in the Android Technical Overview.

| API call: check authentication status |
| --- |
| public void checkAuthentication() |

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** `setAuthenticationStatus()`  

[Back to Android API...](#api)


### getAuthentication {#getAuthN}

**Description:** Starts the full authentication workflow. It starts by checking the authentication status. If not already authenticated, the authentication flow state-machine is started:

- If the last authentication attempt was successful, the MVPD selection phase is skipped and the [*navigateToUrl()*](#navigagteToUrl) callback is triggered. The application uses this callback to instantiate the WebView control that presents the user with the MVPD's login page.
- If the last authentication attempt was unsuccessful or if the user explicitly logged out, the [*displayProviderDialog()*](#displayProviderDialog) callback is triggered. Your application uses this callback to display the MVPD selection UI. Also your app is required to resume the authentication flow by informing the Access Enabler library about the user's MVPD selection via the [setSelectedProvider()](#setSelectedProvider) method.

As the user's credentials are verified on the MVPD login page, your application is required to monitor the multiple redirection operations that take place while the user authenticates at the MVPD's login page. When the correct credentials are entered, the WebView control is redirected to a custom URL defined by the *AccessEnabler.ADOBEPASS\_REDIRECT\_URL* constant. This URL is not intended to be loaded by the WebView. The application must intercept this URL and interpret this event as a signal that the login phase is complete. It should then hand over control to the Access Enabler in order to complete the authentication flow (by calling the *getAuthenticationToken()* method).

If an MVPD supports the "Authentication per Requestor" feature, then multiple authentication tokens can be stored on a device (one per Programmer).  For details on this feature, see the [Caching Guidelines](#$caching) section in the Android Technical Overview.

Finally, the authentication status is communicated to the application via the *setAuthenticationStatus()* callback.



| API call: initiates the authentication flow |
| --- |
| public void getAuthentication() |

**Availability:** v1.0+

| API call: initiates the authentication flow |
| --- |
| public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData) |

**Availability:** v1.8+

**Parameters:**

- *forceAuthn*: A flag that specifies if the authentication flow should be started, regardless if the user is already authenticated or not.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK.

**Callbacks triggered:** `setAuthenticationStatus(), displayProviderDialog(), navigateToUrl(), sendTrackingData()`


[Back to Android API...](#api)

### displayProviderDialog {#displayProviderDialog}

**Description** Callback triggered triggered by the Access Enabler to inform the application that the appropriate UI elements need to be instantiated to allow the user to select the desired MVPD. The callback provides a list of MVPD objects with additional information that can help to correctly build the selection UI panel (such as the URL pointing to the MVPD's logo, friendly display name, etc.)

Once the user has selected the desired MVPD, the upper-layer application is required to resume the authentication flow by calling *setSelectedProvider()* and passing it the ID of the MVPD corresponding to the user's selection.  
 
>[!NOTE]
>
> Aborting the authentication flow
> </br></br>
> Please note that this is a point where the user has the ability to press the "Back" button, which is equivalent to the aborting of the authentication flow. In such a scenario, your application is required to call the `setSelectedProvider()` method, passing *null* as the parameter, to give the Access Enabler the opportunity to reset its authentication state-machine.

| Callback: display the MVPD selection UI |
| --- |
| `public void displayProviderDialog(ArrayList<Mvpd> mvpds)` |

**Availability:** v1.0+

**Parameters**:

- *mvpds*: List of MVPD objects holding MVPD-related information that the application can use to build the MVPD selection UI elements.

**Triggered by:** `getAuthentication(), getAuthorization()`  

[Back to Android API...](#api)


### setSelectedProvider {#setSelectedProvider}

**Description:** This method is called by your application to inform the Access Enabler of the user's MVPD selection. The application can use this method to select or change the service provider used for authentication.

If the MVPD selected is a TempPass MVPD it will automatically authenticate with that MVPD without needing to call getAuthentication() afterwards.

Please note that this is not possible for Promotional Temp Pass where extra parameters are given on getAuthentication() method.

When passing *null* as a parameter, the Access Enabler assumes that the user has canceled the authentication flow (i.e. pressed the "Back" button), and responds by resetting the authentication state-machine and by calling the *setAuthenticationStatus()* callback with the `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` error code.

| API call: set the currently selected provider |
| --- |
| public void setSelectedProvider(String mvpdId) |

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** `setAuthenticationStatus(), sendTrackingData(), navigateToUrl()`  

[Back to Android API...](#api)


### navigateToUrl {#navigagteToUrl}

**Deprecated:** Starting with Android SDK 3.0, navigateToUrl is used only if Chrome Custom Tab is not present on the device

**Description:** Callback triggered by the Access Enabler which informs the application that the user needs to be presented with the MVPD login page in order to enter his credentials. The Access Enabler passes as a parameter the URL of the MVPD login page. Your application is required to instantiate a WebView control and direct it to this URL. Also, the application is required to monitor the URLs loaded by the WebView control and intercept the redirection operation targeting the custom URL defined by the `AccessEnabler.ADOBEPASS_REDIRECT_URL (deprecated)` constant. Upon this event, the application is required to either close or hide the WebView control and yield the control back to the Access Enabler library by calling the *getAuthenticationToken()* method. The Access Enabler completes the authentication flow by retrieving the authentication token from the back-end server and storing it locally in the token storage.  

>[!WARNING]
>
> **Aborting the authentication flow**  <br>Please note that this is a point where the user has the ability to press the "Back" button, which is equivalent to the aborting of the authentication flow. In such a scenario, your application is required to call the _setSelectedProvider()_ method passing _null_ as the parameter and giving a chance to the Access Enabler to reset its authentication state-machine.

| Callback: display MVPD login page |
| --- |
| public void navigateToUrl(String url) |

**Availability:** v1.0+

**Parameters:**

- *url*: The URL pointing to the MVPD's login page
  
**Triggered by:** `getAuthentication(), setSelectedProvider()`  

[Back to Android API...](#api)


### getAuthenticationToken {#getAuthNToken}

**Deprecated:** Starting with Android SDK 3.0, as Chrome Custom Tab is used for authentication, this method is no longer used from the application.

**Description:** Completes the authentication flow by requesting the authentication token from the back-end server. This method should be called by your application only in response to event where the WebView control hosting the MVPD login page is redirected to the custom URL defined by the `AccessEnabler.ADOBEPASS_REDIRECT_URL` constant.

| API call: retrieve the authentication token |
| --- |
| public void getAuthenticationToken() |

**Availability:** v1.0+

**Parameters:**

- *cookies*: Cookies that are set on the the target domain (see the demo application in the SDK for a reference implementation).

**Callbacks triggered:** `setAuthenticationStatus()`, `sendTrackingData()`

[Back to Android API...](#api)


### setAuthenticationStatus {#setAuthNStatus}

**Description:** Callback triggered by the Access Enabler which informs
the application of the status of the authentication flow. There are many
places where this flow can fail, either as a result of user's
interaction or due to other unforeseen scenarios (i.e. network
connectivity problems, etc.). This callback informs the application of
the success/failure status of the authentication flow, while also
providing additional information about the failure reason, when needed.

| Callback: report the status of the authentication flow |
| --- |
| public void setAuthenticationStatus(int status, String errorCode) |

**Availability:** v1.0+

**Parameters:**

- *status*: Can take one of the following values:
    - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS` - authentication flow was successfully completed
    - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR` - authentication flow failed
- *code*: Failure reason. If *status* is `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`, then *code* is an empty string (i.e., defined by the `AccessEnablerConstants.USER_AUTHENTICATED` constant). In case of failure, this parameter can take one of the following values:
    - `AccessEnablerConstants.USER_NOT_AUTHENTICATED_ERROR` - The user is not authenticated. In response to the *checkAuthentication()* method call when there is no valid authentication token in the local token cache.
    - `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` - The AccessEnabler has reset the authentication state-machine after the upper-layer application passed *null* to `setSelectedProvider()` to abort the authentication flow.  Presumably the user has canceled the authentication flow (i.e., pressed the "Back" button).
    - `AccessEnablerConstants.GENERIC_AUTHENTICATION_ERROR` - The authentication flow failed due to reasons such as network unavailability or the user canceled the authentication flow explicitly.

**Triggered by:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

[Back to Android API...](#api)


### checkPreauthorizedResources {#checkPreauth}

>**Deprecated:** Starting with Android SDK 3.6, preauthorize API is replacing checkPreauthorizedResources, providing extended error codes. 

**Description:** This method is used by the application to determine if the user is already authorized to view specific protected resources. The primary purpose of this method is to retrieve information for use in decorating the UI (for example, indicating access status with lock and unlock icons).

| API call: set the currently selected provider |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**Availability:** v1.3+

**Parameters:** The `resources` parameter is an array of resources for which authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it should be an agreed upon value established between the Programmer and the MVPD or a media RSS fragment.

**Callback triggered:** `preauthorizedResources()`

[Back to Android API...](#api)


### checkPreauthorizedResources {#checkPreauth2}

**Deprecated:** Starting with Android SDK 3.6, preauthorize API is replacing checkPreauthorizedResources, providing extended error codes. 

**Description:** This method is used by the application to determine if the user is already authorized to view specific protected resources. The primary purpose of this method is to retrieve information for use in decorating the UI (for example, indicating access status with lock and unlock icons).

| API call: set the currently selected provider |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources, boolean cache)` |

**Availability:** v3.1+

**Parameters:** The `resources` parameter is an array of resources for which authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization()` call, that is, it should be an agreed upon value established between the Programmer and the MVPD or a media RSS fragment.

The `cache` parameter specifies if cached preauthorization response can be used or not. By default cache is true, the SDK will return a previously cached response if available.

**Callback triggered:** `preauthorizedResources()`

[Back to Android API...](#api)

### preauthorizedResources {#preauthResources}

**Deprecated:** Starting with Android SDK 3.6, preauthorize API is replacing checkPreauthorizedResources, providing extended error codes. preauthorizedResources callback will not be called on the new API.


**Description:** Callback triggered by checkPreauthorizedResources(). Provides a list of resources the user is already authorized to view.

| API call: set the currently selected provider |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**Availability:** v1.3+

**Parameters:** The `resources` parameter is an array of resources for which the user is already authorized to view.

**Triggered by:** `checkPreauthorizedResources()`

[Back to Android API...](#api)

### <span id="checkAuthZ"></span>checkAuthorization

**Description:** This method is used by the application to check the authorization status. It starts by checking the authentication status first. If not authenticated, the *setTokenRequestFailed()* callback is triggered, and the method exits. If the user is authenticated, it also triggers the authorization flow. See details on the *getAuthorization()* method.

| API call: check authorization status |
| --- |
| public void checkAuthorization(String resourceId) |

**Availability:** v1.0+

| API call: check authorization status |
| --- |
| public void checkAuthorization(String resourceId, Map<String, Object> genericData) |

**Availability:** v1.8+

**Parameters:**

- *resourceId*: The ID of the resource for which the user requests authorization.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK.

**Callbacks triggered:** `tokenRequestFailed(), setToken(),sendTrackingData(), setAuthenticationStatus()`  

[Back to Android API...](#api)


### <span id="getAuthZ"></span>getAuthorization

**Description:** This method is used by the application to initiate the authorization flow. If the user is not already authenticated, it also initiates the authentication flow. If the user gets authenticated, the Access Enabler proceeds to issue requests for the authorization token (if no valid authorization token is present in the local token cache) and for the short-lived media token. Once the short media token is obtained, the authorization flow is considered complete. The *setToken()* callback gets triggered and the short media token is delivered as a parameter to the application. If for any reason, the authorization fails, the *tokenRequestFailed()* callback is triggered and the error code and details are provided.

| API call: initiate the authorization flow |
| --- |
| public void getAuthorization(String resourceId) |

**Availability:** v1.0+

| API call: initiate the authorization flow |
| --- |
| public void getAuthorization(String resourceId, Map<String, Object> genericData) |

**Availability:** v1.8+

**Parameters:**

- *resourceId*: The ID of the resource for which the user requests authorization.
- *data*: A Map consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 

**Callbacks triggered:** `tokenRequestFailed(), setToken(), sendTrackingData()`  

>[!WARNING]
>
> **Additional callbacks triggered**  <br> This method can also trigger the following callbacks (if the authentication flow is also initiated): *setAuthenticationStatus()*, *displayProviderDialog()*, *navigateToUrl()*

**NOTE: Please use checkAuthorization() instead of getAuthorization() whenever possible. The getAuthorization() method will start a full authentication flow (if the user is not authenticated) and this could lead to a complicated implementation on the Programmer's side.**

[Back to Android API...](#api)


### setToken {#setToken}

**Description:** Callback triggered by the Access Enabler that informs your application that the authorization flow was completed successfully. The short-lived media token is also delivered as a parameter.

| Callback: authorization flow completed successfully |
| --- |
| public void setToken(String token, String resourceId) |

**Availability:** v1.0+

**Parameters:**

- *token*: The short-lived media token
- *resourceId*: The resource for which the authorization was obtained

**Triggered by:** `checkAuthorization()`, `getAuthorization()`  


[Back to Android API...](#api)

### tokenRequestFailed {#tokenRequestFailed}

**Description:** Callback triggered by the Access Enabler that informs the upper-layer application that the authorization flow failed.

| Callback: authorization flow failed |
| --- |
| public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription) |

**Availability:** v1.0+

**Parameters:**

- *resourceId*: The resource for which the authorization was obtained
- *errorCode*: Error code associated to the failure scenario. Possible values:
    - `AccessEnablerConstants.USER_NOT_AUTHORIZED_ERROR` - The user was not able to authorize for the given resource
- *errorDescription*: Additional details about the failure scenario. If this descriptive string is not available for any reason, Adobe Pass authentication sends an empty string **("")**.

  This string can be used by an MVPD to pass custom error messages or sales-related messages. For example, if a subscriber is denied authorization for a resource, the MVPD could send a message such as: "You currently do not have access to this channel in your package. If you would like to upgrade your package click here." The message is passed by Adobe Pass authentication through this callback to the Programmer, who has the option to display or ignore it. Adobe Pass authentication can also use this parameter to provide notification of the condition that might have led to an error. For example, "A network error occurred when communicating with the provider's authorization service."

**Triggered by:** `checkAuthorization(), getAuthorization()`

[Back to Android API...](#api)

### logout {#logout}

**Description:** Use this method to initiate the logout flow. The logout is the result of a series of HTTP-redirect operations due to the fact that the user needs to be logged out from both Adobe Pass authentication servers and also from the MVPD's servers. As a result, this flow cannot be completed with a simple HTTP request issued by the Access Enabler library. A Chrome Custom Tabs is used by the SDK to execute the HTTP-redirect operations. This flow will be visible to the user and closed when complete

| API call: initiate the logout flow |
| --- |
| public void logout() |

**Availability:** v1.0+

**Parameters:** None
  
**Callbacks triggered:**

- `navigateToUrl()` for SDK version prior to 3.0
- `setAuthenticationStatus()` for SDK version > 3.0


[Back to Android API...](#api)


### getSelectedProvider {#getSelectedProvider}

**Description:** Use this method to determine the currently selected provider.

| API call: determine the currently selected MVPD |
| --- |
| public void getSelectedProvider() |

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** `selectedProvider()`

[Back to Android API...](#api)


### <span id="selectedProvider"></span>selectedProvider

**Description:** Callback triggered by the Access Enabler that delivers information about the currently selected MVPD to the application.

| Callback: information about the currently selected MVPD |
| --- |
| public void selectedProvider(Mvpd mvpd) |


**Availability:** v1.0+

**Parameters:**

- *mvpd*: Object containing information about the currently selected MVPD

**Triggered by:** `getSelectedProvider()`

[Back to Android API...](#api)


### getMetadata {#getMetadata}

**Description:** Use this method to retrieve information exposed as metadata by the Access Enabler library. The application can access this information by providing a composite MetadataKey object.

| API call: query the AccessEnabler for metadata |
| --- |
| `public void getMetadata(MetadataKey metadataKey)` |

**Availability:** v1.0+

There are two types of metadata available to Programmers:

- Static metadata (Authentication token TTL, Authorization token TTL and Device ID) 
- User metadata (User-specific information, such as User ID and Zip Code; passed from an MVPD to a user's device during the Authentication and / or Authorization flows)

**Parameters:**

- *metadataKey*: A data structure that encapsulates a key and args variable, with the following meaning:
    - If key is `METADATA_KEY_USER_META` and args contains a SerializableNameValuePair object with name = `METADATA_ARG_USER_META` and value = `[metadata_name]`, then the query is made for user metadata. The current list of available user metadata types:
        - `zip` - Zip Code
      
        - `householdID` - Household identifier. If an MVPD does not support subaccounts, this will be identical to `userID`.
      
        - `maxRating` - Maximum parental rating for the user
      
        - `userID` - The user identifier. If an MVPD supports subaccounts, and the user is not the main account, `userID` will be different than `householdID`.
      
        - `channelID` - A list of channels the user is entitled to view
    - If key is `METADATA_KEY_DEVICE_ID` then the query is made to obtain the current device id. Note that this feature is disabled by default and Programmers should contact Adobe for information regarding enablement and fees.
    - If key is `METADATA_KEY_TTL_AUTHZ` and args contains a SerializableNameValuePair object with name = `METADATA_ARG_RESOURCE_ID` and value = `[resource_id]`, then the query is made to obtain the expiration time of the authorization token associated to the specified resource.
    - If key is `METADATA_KEY_TTL_AUTHN` then the query is made to obtain the authentication token expiration time. 

 

>[!NOTE]
>
>For SDK 3.4.0, the constants : `METADATA_KEY_USER_META, METADATA_KEY_DEVICE_ID, METADATA_KEY_TTL_AUTHZ, METADATA_KEY_TTL_AUTHN` are available from com.adobe.adobepass.accessenabler.api.profile.UserProfileService.



>[!NOTE]
>
>The actual User Metadata available to a Programmer depends on what an MVPD makes available.  This list will be further expanded as new metadata is made available and added into the Adobe Pass authentication system.

**Callbacks triggered:** [`setMetadataStatus()`](#setMetadaStatus)

**More Information:** [User Metadata](/help/authentication/user-metadata-feature.md)

[Back to Android API...](#api)

### setMetadataStatus {#setMetadaStatus}

**Description:** Callback triggered by the Access Enabler that delivers the metadata requested via a *getMetadata()* call.

| Callback: result of metadata retrieval request |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Availability:** v1.0+

**Parameters:**

- *key*: The MetadataKey object containing the key for which metadata value is requested and associated parameters (see demo application for a reference implementation).
- *result*: A composite object containing the requested metadata. The object has the following fields:
    - *simpleResult*: a String that represents the metadata value when the request was made for Authentication TTL, Authorization TTL, or Device ID. This value is null if the request was made for User Metadata.
  
    - *userMetadataResult*: an Object that contains the Java representation of a JSON User Metadata payload.  
    For example:
      
```json
          '{
          "street": "Main Avenue",
          "buildings": ["150", "320"]
          }'
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

- *encrypted*: Boolean value that specifies whether the retrieved metadata is encrypted or not. This parameter is significant only for User Metadata requests, it has no meaning for Static Metadata (e.g.: Authentication TTL) that is always received unencrypted. If this parameter is set to True, then it's up to the Programmer to obtain the unencrypted User Metadata value by performing an RSA decryption using the whitelisting private key (the same private key that is used for the signing of the requestor id in the [`setRequestor`](#setRequestor) call).

**Triggered by:** [`getMetadata()`](#getMetadata)

**More Information:** [User Metadata](/help/authentication/user-metadata-feature.md)


[Back to Android API...](#api)


### getVersion {#getVersion}

**Description:** This method can be used to retrieve the version of the AccessEnabler library.

| API call: get AccessEnabler version |
| --- |
| ```public static String getVersion()``` |


[Back to Android API...](#api)

</br>

## Tracking Events {#tracking}

The Access Enabler triggers an additional callback that is not necessarily related to the entitlement flows. Implementing the event-tracking callback function named *sendTrackingData()* is optional, but it enables the application to track specific events and compile statistics such as number of successful/failed authentication/authorization attempts. Below is the specification for the *sendTrackingData()* callback:  
 

### sendTrackingData {#sendTrackingData}

**Description:** Callback triggered by the Access Enabler signaling to the application the occurrence of various events such as the completion/failure of authentication/authorization flows. The device type, Access Enabler client type, and operating system are also reported by sendTrackingData().

>[!WARNING]
>
> The device type and operating system are derived through the use of a public Java library ([http://java.net/projects/user-agent-utils](http://java.net/projects/user-agent-utils)) and the user agent string. Be advised that this information is provided only as a coarse way to break down operational metrics into device categories, but that Adobe can take no responsibility for incorrect results. Please use the new functionality accordingly.


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
    - `android`

</br>

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

Following are instructions for interpreting the values in the *data*
array:

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

**Triggered by:** `checkAuthentication()`, `getAuthentication()`, `checkAuthorization()`, `getAuthorization()`, `setSelectedProvider()`

[Back to Android API...](#api)


<!--
## Related Information {#related}

- [Android Integration Cookbook](/help/authentication/android-sdk-cookbook.md)
- [Android Technical Overview](/help/authentication/android-sdk-overview.md)

-->
