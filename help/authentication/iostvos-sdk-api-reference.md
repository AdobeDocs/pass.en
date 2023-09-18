---
title: iOS/tvOS API Reference
description: iOS/tvOS API Reference
exl-id: 017a55a8-0855-4c52-aad0-d3d597996fcb
---
# iOS/tvOS SDK API Reference {#iostvos-sdk-api-reference}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

This page describes the methods and callback functions exposed by the iOS/tvOS native client for Adobe Pass Authentication. The methods and callback functions described here are defined in the `AccessEnabler.h` and `EntitlementDelegate.h` header files; you can find them in the iOS AccessEnabler SDK here: `[SDK directory]/AccessEnabler/headers/api/`


Associated documentation:

*   For a description of the basic Adobe Pass Authentication entitlement flow, see [Entitlement Flow](/help/authentication/entitlement-flow.md).
*   For a step-by-step walkthough of how to implement the Adobe Pass
  authentication entitlement flow using this API, see the [iOS Integration Cookbook](/help/authentication/iostvos-sdk-cookbook.md).
*   For the latest iOS AccessEnabler SDK, see [iOS Native Access Enabler Library](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

>[!NOTE]
>
>Adobe encourages you to use only the Adobe Pass Authentication *public* APIs:
>
>* Public APIs are available and fully tested on all supported client types. For any public feature, we make sure that each client type has a corresponding version of the associated method(s).
>* Public APIs are required to be as stable as possible, to support backwards compatibility and ensure that partner integrations do not break. However, for non-public APIs, we reserve the right to change their signature at any future point. If you encounter a particular flow that cannot be supported through a combination of the current public Adobe Pass Authentication API calls, the best approach is to let us know. Taking into account your needs, we can modify the public APIs and provide a stable solution moving forward.

</br>

## API Reference {#apis}

* [init](#initWithSoftwareStatement):softwareStatement - Instantiates the AccessEnabler object.

* **[DEPRECATED]** [init](#init) - Instantiates the AccessEnabler object.

* [setOptions:options:](#setOptions) - Configures global SDK options like profile or visitorID.

* [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3) - Establishes the identity of the Programmer.

* **[DEPRECATED]** [setRequestor:signedRequestorId:](#setReq),[setRequestor:signedRequestorId:serviceProviders:](#setReq) - Establishes the identity of the Programmer.

* **[DEPRECATED]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos)-Establishes the identity of the Programmer.

* [setRequestorComplete:](#setReqComplete) - Informs your application that the configuration phase is complete.

* [checkAuthentication](#checkAuthN) - Checks the authentication status of the current user.

* [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN) - Starts the full authentication workflow.

* [getAuthentication:filter](#getAuthN_filter),[getAuthentication:withData:](#getAuthN)[andFilter](#getAuthN_filter) - Starts the full authentication workflow.

* [displayProviderDialog:](#dispProvDialog) - Informs your application to instantiate the appropriate UI elements for the user to select an MVPD.

* [setSelectedProvider:](#setSelProv) - Informs the AccessEnabler of the user's MVPD selection.

* [navigateToUrl:](#nav2url) - Informs your application that the user needs to be presented with the MVPD login page.

* [navigateToUrl:useSVC:](#nav2urlSVC) - Informs your application that the user needs to be presented with the MVPD login page, using SFSafariViewController

* [handleExternalURL:url](#handleExternalURL) - Completes the authentication/logout flow.

* **[DEPRECATED]** [getAuthenticationToken](#getAuthNToken) - Requests the authentication token from the back-end server.

* [setAuthenticationStatus:errorCode:](#setAuthNStatus) - Informs your application of the status of the authentication flow.

* [checkPreauthorizedResources:](#checkPreauth) - Determines if the user is already authorized to view specific protected resources.

* [checkPreauthorizedResources:cache:](#checkPreauthCache) - Determines if the user is already authorized to view specific protected resources.

* [preauthorizedResources:](#preauthResources) - Provides a list of resources the user is already authorized to view.

* [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ) - Checks the authorization status of the current user.

* [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ) - Initiates the authorization flow.

* [setToken:forResource:](#setToken) - Informs your application that the authorization flow was completed successfully.

* [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) - Informs your application that the authorization flow failed.

* [logout](#logout) - Initiates the logout flow.

* [getSelectedProvider](#getSelProv) - Determines the currently selected provider.

* [selectedProvider:](#selProv) - Delivers information about the currently selected MVPD to your application.

* [getMetadata:](#getMeta) - Retrieves information exposed as metadata by the AccessEnabler library.

* [presentTvProviderDialog:](#presentTvDialog) - Informs your application to display the Apple SSO Dialog.

* [dismissTvProviderDialog:](#dismissTvDialog) - Informs your application to hide the Apple SSO Dialog.

* [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus) - Delivers the metadata requested by a [getMetadata:](#getMeta) call.

* [sendTrackingData:forEventType:](#sendTracking) - Delivers tracking data information.

* [MVPD](#mvpd) - The MVPD class. [Contains information about the MVPD]

### init:softwareStatement {#initWithSoftwareStatement}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Instantiates the AccessEnabler object. There should be a single AccessEnabler instance per application instance.

| **API call: iOS AccessEnabler constructor** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**Availability:** v3.0+

**Parameters:**

* **softwareStatement:** A string that identifies the application in Adobe's system. Check out how to obtain a Software Statement.

[Back to top...](#apis)



### init - [DEPRECATED]{#init}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Instantiates the AccessEnabler object. There should be a single AccessEnabler instance per application instance.

| API call: iOS AccessEnabler constructor |
| --- |
| ```- (id) init;``` |

**Availability:** v1.0+ **Until:** v3.0

**Parameters:** None

[Back to top...](#apis)

</br>

### setOptions:options {#setOptions}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Configures global SDK options. It accepts an NSDictionary as an argument. The values from the dictionary will be passed to the server along with every network call that the SDK makes.

**Note:** The values will be passed to the server independent of the current flow (authentication/authorization). If you want to change the values you can call this method at any point in time.

| API call: setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**Availability:** v2.3.0+

**Parameters:**

* *options*: An NSDictionary containing global SDK options. Currently, the following options are available:
  * **applicationProfile** - It can be used to make server configurations based on this value.
  * **visitorID** - The Marketing Cloud visitorID. This value can be later used for advanced analytics reports.
  * **handleSVC** - Boolean indicating if the programmer will handle the SFSafariViewControllers. Please see [SFSafariViewController support on iOS SDK 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) for more details.
    * If set to **false,** the SDK will automatically present the end user with an SFSafariViewController. The SDK will further navigate to the MVPDs login page URL.
    * If set to **true,** the SDK will **NOT** automatically present the end user with an SFSafariViewController. The SDK will further trigger **navigate(toUrl:{url}, useSVC:YES)**.
* **device\_info** - Client information as described in [Passing client information](/help/authentication/passing-client-information-device-connection-and-application.md).

[Back to top...](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Establishes the identity of the Programmer. Each Programmer is assigned a unique ID upon registering with Adobe for the Adobe Pass Authentication system. When dealing with SSO and remote tokens, the authentication state can change when the application is in the background, setRequestor can be called again when the application is brought into the foreground in order to synchronize with the system state (fetch a remote token if SSO is enabled or delete the local token if a logout happened in the meantime).

The server response contains a list of MVPDs together with some configuration information that is attached to the identity of the Programmer. The server response is used internally by the AccessEnabler code. Only the status of the operation (i.e., SUCCESS/FAIL) is presented to your application via the `setRequestorComplete:` callback.  

If the `urls` parameter is not used, the resulting network call targets the default service provider URL: the Adobe RELEASE/production environment.  


If a value is provided for the `urls` parameter, the resulting network call targets all of the URLs provided in the `urls` parameter. All configuration requests are triggered simultaneously in separate threads. The first responder takes precedence when compiling the list of MVPDs. For each MVPD in the list, the AccessEnabler remembers the URL of the associated service provider. All subsequent entitlement requests are directed to the URL associated with the service provider that was paired with the target MVPD during the configuration phase.

| API call: requestor configuration |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**Availability:** v3.0+

| API call: requestor configuration |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**Availability:** v3.0+

**Parameters:**

* *requestorID*: The unique ID associated with the Programmer. Pass the unique ID assigned by Adobe to your site when you first register  with the Adobe Pass Authentication service.
* *urls*: Optional parameter; by default, the Adobe service provider is used (http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass Authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.

>[!NOTE]
>
>If called without the `serviceProviders` parameter, the library will retrieve the configuration from the default service provider (that is, `https://sp.auth.adobe.com` for the production profile or `https://sp.auth-staging.adobe.com` for the staging profile). If the `serviceProviders` parameter is provided, it must be an array of URL's. The configuration information is retrieved from all specified endpoints and is merged. If duplicate information exists in different service provider responses, the conflict is resolved in favor of the fastest responding server (that is, the server with the shortest response time takes precedence).

**Callbacks triggered:** [`setRequestorComplete:`](#setReqComplete)

[Back to top...](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:serviceProviders: - [DEPRECATED] {#setReq}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Establishes the identity of the Programmer. Each Programmer is assigned a unique ID upon registering with Adobe for the Adobe Pass Authentication system. When dealing with SSO and remote tokens the authentication state can change when the application is in the background, setRequestor can be called again when the application is brought into foreground in order to synchronize with the system state (fetch a remote token if SSO is enabled or delete the local token if a logout happened in the meantime).

The server response contains a list of MVPDs together with some configuration information that is attached to the identity of the Programmer. The server response is used internally by the AccessEnabler code. Only the status of the operation (i.e., SUCCESS/FAIL) is presented to your application via the `setRequestorComplete:` callback.  

If the `urls` parameter is not used, the resulting network call targets the default service provider URL: the Adobe RELEASE/production environment.  

If a value is provided for the `urls` parameter, the resulting network call targets all of the URLs provided in the `urls` parameter. All configuration requests are triggered simultaneously in separate threads. The first responder takes precedence when compiling the list of MVPDs. For each MVPD in the list, the AccessEnabler remembers the URL of the associated service provider. All subsequent entitlement requests are directed to the URL associated with the service provider that was paired with the target MVPD during the configuration phase.

| API call: requestor configuration |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br>|

**Availability:** v1.0+ **Until:** v3.0

| API call: requestor configuration |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**Availability:** v1.0+ **Until:** v3.0

**Parameters:**

* *requestorID*: The unique ID associated with the Programmer. Pass the unique ID assigned by Adobe to your site when you first registered with the Adobe Pass Authentication service. 
* *signedRequestorID*: **This parameter exists in iOS AccessEnabler versions 1.2 and later.** A copy of the requestor ID that is digitally signed with your private key. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *urls*: Optional parameter; by default, the Adobe service provider is used (http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass Authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.

**Notes:** If called without the `serviceProviders` parameter, the library will retrieve the configuration from the default service provider (that is,`https://sp.auth.adobe.com` for the production profile or `https://sp.auth-staging.adobe.com` for the staging profile). If the `serviceProviders` parameter is provided, it must be an array of URL's. The configuration information is retrieved from all specified endpoints and is merged. If duplicate information exists in different service provider responses, the conflict is resolved in favor of the fastest responding server (i.e., the server with the shortest response time takes precedence).

**Callbacks triggered:** [`setRequestorComplete:`](#setReqComplete)


[Back to top...](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [DEPRECATED] {#setReq_tvos}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Establishes the identity of the Programmer. Each Programmer is assigned a unique ID upon registering with Adobe for the Adobe Pass Authentication system. This setting should be performed only once during the application's life cycle.

The server response contains a list of MVPDs together with some configuration information that is attached to the identity of the Programmer. The server response is used internally by the AccessEnabler code. Only the status of the operation (i.e., SUCCESS/FAIL) is presented to your application via the `setRequestorComplete:` callback.  

If the `urls` parameter is not used, the resulting network call targets the default service provider URL: the Adobe RELEASE/production environment.  

If a value is provided for the `urls` parameter, the resulting network call targets all of the URLs provided in the `urls` parameter. All configuration requests are triggered simultaneously in separate threads. The first responder takes precedence when compiling the list of MVPDs. For each MVPD in the list, the AccessEnabler remembers the URL of the associated service provider. All subsequent entitlement requests are directed to the URL associated with the service provider that was paired with the target MVPD during the configuration phase.



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: requestor configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**Availability:** v2.0+ **Until:** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: requestor configuration</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**Availability:** v2.0+ **Until:** v3.0

**Parameters:**

* *requestorID*: The unique ID associated with the Programmer. Pass the unique ID assigned by Adobe to your site when you first   registered with the Adobe Pass Authentication service. 
* *signedRequestorID*: **This parameter exists in iOS AccessEnabler   versions 1.2 and later.** A copy of the requestor ID that is digitally signed with your private key. <!--For more details, see [Registering Native Clients](https://tve.helpdocsonline.com/registering-native-clients)-->.
* *urls*: Optional parameter; by default, the Adobe service provider   is used (http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass Authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.
* secret and publicKey: The secret and public key used to sign the second screen calls. For more information see the [Clienteless documentation](#create_dev).

If called without the `serviceProviders` parameter, the library will retrieve the configuration from the default service provider (i.e., `https://sp.auth.adobe.com` for the production profile or https://sp.auth-staging.adobe.com for the staging profile). If the `serviceProviders` parameter is provided, it must be an array of URL's. The configuration information is retrieved from all specified endpoints and is merged. If duplicate information exists in different service provider responses, the conflict is resolved in favor of the fastest responding server (i.e., the server with the shortest response time takes precedence).

**Callbacks triggered:** [`setRequestorComplete:`](#setReqComplete)

[Back to top...](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler that informs your application that the configuration phase is complete. This is a signal that the app can start issuing entitlement requests. No entitlement requests can be issued by the application until the configuration phase is complete.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: requestor configuration complete</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**Availability:** v1.0+

**Parameters**:

* *status*: can take one of the following values:
    * `ACCESS_ENABLER_STATUS_SUCCESS` - configuration phase was successfully completed
    * `ACCESS_ENABLER_STATUS_ERROR` - configuration phase failed

**Triggered by:**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[Back to top...](#apis)

</br>

### checkAuthentication {#checkAuthN}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Checks the authentication status of the current user.
It does this by searching for a valid authentication token in the local
token storage space. Calling this method performs no network calls. It
is used by the application to query the user's authentication status and
update the UI accordingly (i.e., update the login/logout UI). The
authentication status is communicated to the application via
the [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) callback.  
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: check authentication status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[Back to top...](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Starts the full authentication workflow. It starts by checking the authentication status. If not already authenticated, the authentication flow state-machine is started:

* if the last authentication attempt was successful, the MVPD   selection phase is skipped and   the [`navigateToUrl:`](#nav2url) callback is triggered. The   application uses this callback to instantiate the WebView control that presents the user with the MVPD's login page. **[NOTE: As of Acccess Enabler 1.5, this functionality is unavailable because of a limitation in the SDK].**
* if the last authentication attempt was unsuccessful or if the user explicitly logged out, the [`displayProviderDialog:`](#dispProvDialog) callback is   triggered. Your application uses this callback to display the MVPD selection UI. Also your app is required to resume the authentication flow by informing the AccessEnabler library about the user's MVPD selection via the [`setSelectedProvider:`](#setSelProv) method.

As the user's credentials are verified on the MVPD login page, your application is required to monitor the multiple redirection operations that take place while the user authenticates at the MVPD's login page. When the correct credentials are entered, the WebView control is redirected to a custom URL defined by the `ADOBEPASS_REDIRECT_URL` constant. This URL is not intended to be loaded by the WebView. The application must intercept this URL and interpret this event as a signal that the login phase is complete. It should then hand over control to the AccessEnabler in order to complete the authentication flow (by calling the [handleExternalURL](#handleExternalURL) method).  

Finally, the authentication status is communicated to the application via the [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Availability:** v1.9+

**Parameters:**

* *forceAuthn*: A flag that specifies if the authentication flow should be started, regardless if the user is already authenticated or not.
* *data*: A dictionary consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK.

**Callbacks triggered:** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`

  
[Back to top...](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:andFilter {#getAuthN_filter}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Starts the full authentication workflow. It starts by checking the authentication status. If not already authenticated, the authentication flow state-machine is started:

* [presentTvProviderDialog()](#presentTvDialog) will be called if the current requestor has at least one MVPD that supports SSO. If no MVPD supports SSO, the classic authentication flow will begin and the filter parameter is ignored.
* After the user completes the Apple SSO flow [dismissTvProviderDialog()](#dismissTvDialog) will be triggered and the authentication process will finish.

Finally, the authentication status is communicated to the application via the [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback.

**Availability:** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parameters:**

* *forceAuthn*: A flag that specifies if the authentication flow should be started, regardless if the user is already authenticated or not.
* *data*: A dictionary consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 
* filter: A dictionary with two lists of MVPD ids that should appear in the Apple SSO Dialog. Any MVPD that does not support SSO will be ignored but the order will be respected. The dictionary needs to have two keys:
    * TV\_PROVIDERS: A list with all MVPDs that should appear in the picker
    * FEATURED\_TV\_PROVIDERS: A list with all MVPDs that should be marked as featured in the picker. MVPDs in this list must also be specified in the TV\_PROVIDERS list.

**Availability:** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiates the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parameters:**

* *forceAuthn*: A flag that specifies if the authentication flow should be started, regardless if the user is already authenticated or not.
* *data*: A dictionary consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 
* filter: A list of MVPD ids that should appear in the Apple SSO Dialog. Any MVPD that does not support SSO will be ignored but the order will be respected.

**Callbacks triggered:** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`

  
[Back to top...](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered triggered by the AccessEnabler to inform the application that the appropriate UI elements need to be instantiated to allow the user to select the desired MVPD. The callback provides a list of MVPD objects with additional information that can help to correctly build the selection UI panel (such as the URL pointing to the MVPD's logo, friendly display name, etc.)  

Once the user has selected the desired MVPD, the upper-layer application is required to resume the authentication flow by calling `setSelectedProvider:` and passing it the ID of the MVPD corresponding to the user's selection.

**Aborting the authentication flow** - This is a point where the user has the ability to press the "Back" button, which is equivalent to aborting the authentication flow. In that scenario, your application is required to call the [setSelectedProvider:](#setSelProv) method, passing null as the parameter, to give the AccessEnabler the opportunity to reset its authentication state-machine.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: display the MVPD selection UI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**Availability:** v1.0+

**Parameters**:

* *mvpds*: list of MVPD objects holding MVPD-related information that the application can use to build the MVPD selection UI elements.

**Triggered by:** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[Back to top...](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is called by your application to inform the Access Enabler of the user's MVPD selection. The application can use this method to select or change the service provider used for authentication.

If the MVPD selected is a TempPass MVPD it will automatically authenticate with that MVPD without needing to call getAuthentication() afterwards.

Please note that this is not possible for Promotional Temp Pass where extra parameters are given on getAuthentication() method.

When passing *null* as a parameter, the Access Enabler assumes that the user has canceled the authentication flow (i.e. pressed the "Back" button), and responds by resetting the authentication state-machine and by calling the [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback with the `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` error code.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: set the currently selected provider</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)  

[Back to top...](#apis)

</br>

#### navigateToUrl: {#nav2url}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description:** Callback triggered by the AccessEnabler to request your application to instantiate a UIWebView/WKWebView controller and to load the URL provided in the callback's **`url`** parameter. The callback passes the **`url`** parameter which represents the URL of the authentication endpoint or the URL of the logout endpoint.

As the UIWebView/WKWebView` `controller goes through several redirects, your application must monitor the activity of the controller and detect the moment when it loads a specific custom URL defined by the `ADOBEPASS_REDIRECT_URL `constant (i.e. `adobepass://ios.app`). Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the authentication or logout flow has completed and that it is safe to close the controller. When the controller loads this specific custom URL your application must close the UIWebView/WKWebView and call AccessEnabler's `handleExternalURL:url `API method.

  **Note:** Please note that in case of the authetication flow this is a point where the user has the ability to press the "Back" button, which is equivalent to the aborting of the authentication flow. In such a scenario, your application is required to call the [setSelectedProvider:](#setSelProv) method passing **`nil`** as the parameter and giving a chance to the AccessEnabler to reset its authentication state-machine.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: display MVPD login page</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters**:

* *url*: the URL pointing to the MVPD's login page

**Triggered by:** [setSelectedProvider:](#setSelProv)

 

[Back to top...](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description:** Callback triggered by the AccessEnabler instead of the `navigateToUrl:` callback in case your application previously enabled manual Safari View Controller (SVC) handling via the [setOptions(\["handleSVC":true"\])](#setOptions) call, and only in case of MVPDs requiring Safari View Controller (SVC). For all other MVPDs the `navigateToUrl:` callback will be called. Please see[SFSafariViewController support on iOS SDK 3.2+](/help/authentication/sfsafariviewcontroller-support-on-ios-sdk-32.md) for details on how Safari View Controller (SVC) should be managed.

Similar to the `navigateToUrl:` callback the `navigateToUrl:useSVC:` is triggered by the AccessEnabler to request your application to instantiate a `SFSafariViewController` controller and to load the URL provided in the callback's **`url`** parameter. The callback passes the **`url`** parameter which represents the URL of the authentication endpoint or the URL of the logout endpoint, and the **`useSVC`** parameter which specifies that the application must use a `SFSafariViewController`.

As the `SFSafariViewController` controller goes through several redirects, your application must monitor the activity of the controller and detect the moment when it loads a specific custom URL defined by your `application's custom scheme` (e.g.** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`). Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the authentication or logout flow has completed and that it is safe to close the controller. When the controller loads this specific custom URL your application must close the `SFSafariViewController` and call AccessEnabler's `handleExternalURL:url `API method.

  **Note:** Please note that in case of the authetication flow this is a point where the user has the ability to press the "Back" button, which is equivalent to the aborting of the authentication flow. In such a scenario, your application is required to call the [setSelectedProvider:](#setSelProv) method passing **`nil`** as the parameter and giving a chance to the AccessEnabler to reset its authentication state-machine.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: display MVPD login page in SFSafariViewController</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:**v 3.2+

**Parameters**:

* *url:* the URL pointing to the MVPD's login page
* *useSVC:* whether the url should be loaded in SFSafariViewController.

**Triggered by:**[setOptions:](#setOptions) before [setSelectedProvider:](#setSelProv) 

[Back to top...](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is called by your application to complete the authentication or logout flow. This method should be called right after your application detects the moment when the `UIWebView/WKWebView or SFSafariViewController` controller is redirected to a specific custom URL. In case your application is required to use a `SFSafariViewController `controller the specifc custom URL is defined by your `application's custom scheme` (e.g.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the `ADOBEPASS_REDIRECT_URL `constant (i.e. `adobepass://ios.app`).

In case of the authentication flow the AccessEnabler completes the flow by retrieving the authentication token from the back-end server and storing it locally in the token storage. The AccessEnabler will inform your application that the authentication flow is complete by calling the `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> callback with a status code of 1, indicating success. If there is an error during the execution of these steps, the `setAuthenticationStatus()`<!--(http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus)--> callback is triggered with a status code of 0, indicating authentication failure, as well as a corresponding error code.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: complete the authentication or logout flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code> (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v3.0+

**Parameters:** 

* *url*: The intercepted URL from the ` UIWebView/WKWebView or SFSafariViewController ` control as string.


**Callbacks triggered:** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`  

[Back to top...](#apis)

</br>

#### getAuthenticationToken - [DEPRECATED] {#getAuthNToken}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Completes the authentication flow by requesting the authentication token from the back-end server. This method should be called by your application only in response to event where the WebView control hosting the MVPD login page is redirected to the custom URL defined by the `ADOBEPASS_REDIRECT_URL` constant.  
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: retrieve the authentication token</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+ **Until:** v3.0

**Parameters:** None

**Callbacks triggered:** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`  

[Back to top...](#apis)

</br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler which informs the application of the status of the authentication flow. There are many places where this flow can fail, either as a result of user's interaction or due to other unforeseen scenarios (i.e., network connectivity problems, etc.). This callback informs the application of the success/failure status of the authentication flow, while also providing additional information about the failure reason, when needed.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: report the status of the authentication flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**Availability:** v1.0+

**Parameters**:

* *status*: can take one of the following values:
    * `ACCESS_ENABLER_STATUS_SUCCESS` - authentication flow was successfully completed
    * `ACCESS_ENABLER_STATUS_ERROR` - authentication flow failed 
* *code*: failure reason. If *status* is `ACCESS_ENABLER_STATUS_SUCCESS`, then *code* is an empty string (i.e., defined by the `USER_AUTHENTICATED` constant). In case of failure, this parameter can take one of the following values:
    * `USER_NOT_AUTHENTICATED_ERROR` - The user is not authenticated. In response to the [checkAuthentication:](#checkAuthN) method call when there is no valid authentication token in the local token cache.
    * `PROVIDER_NOT_SELECTED_ERROR` - The AccessEnabler has reset the       authentication state-machine after the upper-layer application       passed *null* to [`setSelectedProvider:`](#setSelProv) to abort the authentication flow.  Presumably the user has canceled the authentication flow (i.e., pressed the "Back" button).
    * `GENERIC_AUTHENTICATION_ERROR` - The authentication flow failed due to reasons such as network unavailability or the user canceled the authentication flow explicitly.

**Triggered by:** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[Back to top...](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is used by the application to determine if the user is already authorized to view specific protected resources. The primary purpose of this method is to retrieve information for use in decorating the UI **(for example, indicating access status with lock and unlock icons).**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: set the currently selected provider</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.3+

**Parameters:**

* *resources:* array of resources for which authorization should be checked. Each element in the list should be a string representing the resource ID. The     resource ID is subject to the same limitations as the resource ID in the call, that is, it should be an agreed upon value established between the Programmer and the MVPD or a media RSS fragment.

**Callback triggered:** [`preauthorizedResources:`](#preauthResources)

[Back to top...](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is used by the application to determine if the user is already authorized to view specific protected resources. The primary purpose of this method is to retrieve information for use in decorating the UI (for example, indicating access status with lock and unlock icons). The **cache** parameter controls wether the internal cache is used for resolving resources.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: set the currently selected provider</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**Availability:** v3.1+

 

**Parameters:**

* *resources:* array of resources for which authorization should be checked. Each element in the list should be a string representing the resource ID. The resource ID is subject to the same limitations as the resource ID in the `getAuthorization:` call, that is, it should be an agreed upon value established between the Programmer and the MVPD or a media RSS fragment.
* *cache:* Boolean specifying wether to use the internal cache for resolving resources. If false the cache will be bypassed, resulting in server calls each time this API is called.

**Callback triggered:** [`preauthorizedResources:`](#preauthResources)

[Back to top...](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description:** Callback triggered by `checkPreauthorizedResources:`. Provides a list of resources the user is already authorized to view.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: set the currently selected provider</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.3+

**Parameters:**

* `resources`: array of resources for which the user is already authorized to view.

**Triggered by:** [`checkPreauthorizedResources:`](#checkPreauth)

 

[Back to top...](#apis)

</br>

### checkAuthorization:, checkAuthorization:withData: {#checkAuthZ}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is used by the application to check the authorization status. It starts by checking the authentication status first. If not authenticated, the [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) callback is triggered, and the method exits. If the user is authenticated, it also triggers the authorization flow. See details on the [`getAuthorization:`](#getAuthZ) method.  


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: check authorization status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: check authorization status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.9+

**Parameters:**

* *resource*: the ID of the resource for which the user requests authorization.
* *data*: A dictionary consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 

**Callbacks triggered:**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`  

[Back to top...](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is used by the application to initiate the authorization flow. If the user is not already authenticated, it also initiates the authentication flow. If the user gets authenticated, the AccessEnabler proceeds to issue requests for the authorization token (if no valid authorization token is present in the local token cache) and for the short-lived media token. Once the short media token is obtained, the authorization flow is considered complete. The [setToken:forResource:](#setToken) callback gets triggered and the short media token is delivered as a parameter to the application. If for any reason, the authorization fails, the [tokenRequestFailed:forEventType:](#tokenReqFailed) callback is triggered and the error code/details are provided.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiate the authorization flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiate the authorization flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**Availability:** v1.9+

**Parameters:**

* *resource*: the ID of the resource for which the user requests authorization.
* *data*: A dictionary consisting of key-value pairs to be sent to the Pay-TV pass service. Adobe can use this data to enable future functionality without changing the SDK. 

**Callbacks triggered:** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**Additional callbacks triggered:**  
This method can also trigger the following callbacks (if the authentication flow is also initiated): `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`  
 
**NOTE: Please use checkAuthorization: / checkAuthorization:withData: instead of getAuthorization: / getAuthorization:withData: whenever possible. The getAuthorization: / getAuthorization:withData: method will start a full authentication flow (if the user is not authenticated) and this could lead to a complicated implementation on the Programmer's side.**

[Back to top...](#apis)

</br>

### setToken:forResource: {#setToken}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler that informs your application that the authorization flow was completed successfully. The short-lived media token is also delivered as a parameter.  
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: authorization flow completed successfully</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters**:

* *token*: the short-lived media token
* *resource*: the resource for which the authorization was obtained

**Triggered by:** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[Back to top...](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler that informs the upper-layer application that the authorization flow failed.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: authorization flow failed</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters**:

* *resource*: The resource for which the authorization was obtained.
* *code*: The error code associated with the failure scenario. Possible values:
    * `USER_NOT_AUTHORIZED_ERROR` - the user was not able to authorize
      for the given resource
* *description*: Additional details about the failure scenario. If this descriptive string is not available for any reason, Adobe Pass Authentication sends an empty string **("")**.   
  This string can be used by an MVPD to pass custom error messages or sales-related messages. For example, if a subscriber is denied authorization for a resource, the MVPD could send a message such as: "You currently do not have access to this channel in your package. If you would like to upgrade your package click **here**." The message is passed by Adobe Pass Authentication through this callback to the Programmer, who has the option to display or ignore it. Adobe Pass Authentication can also use this parameter to provide notification of the condition that might have led to an error. For example, "A network error occurred when communicating with the provider's authorization service".

**Triggered by:** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[Back to top...](#apis)

</br>

### logout {#logout}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** This method is called by your application to initiate the logout flow. The logout is the result of a series of HTTP redirect operations due to the fact that the user needs to be logged out from both Adobe Pass Authentication servers and also from the MVPD's servers. Because this flow cannot be completed with a simple HTTP request issued by the AccessEnabler library, a `UIWebView/WKWebView or SFSafariViewController` controller needs to be instantiated in order to be able to follow the HTTP redirect operations.

The logout flow differs from the authentication flow in that the user is not required to interact with the `UIWebView/WKWebView or SFSafariViewController`  controller in any way. Therefore, Adobe recommends that you make the control invisible (i.e. hidden) during the logout process.

A pattern similar with the authentication flow is employed. The iOS AccessEnabler triggers the `navigateToUrl:` callback or the `navigateToUrl:useSVC:` to create a `UIWebView/WKWebView or SFSafariViewController` controller and to load the URL provided in the callback's `url` parameter. This is the URL of the logout endpoint on the backend server. For the tvOS AccessEnabler neither the `navigateToUrl:` callback or the `navigateToUrl:useSVC:` callback is called.

As it goes through several redirects, your application must monitor the activity of the `UIWebView/WKWebView or SFSafariViewController `controller and detect the moment when it loads a specific custom URL. Note that this specific custom URL is actually invalid, and it is not intended for the controller to actually load it. It must be only interpreted by your application as a signal that the logout flow has completed and that it is safe to close the controller. When the controller loads this specific custom URL your application must close the controller and call AccessEnabler's `handleExternalURL:url `API method. In case your application is required to use a `SFSafariViewController `controller the specifc custom URL is defined by your `application's custom scheme` (e.g.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), otherwise this specific custom URL is defined by the `ADOBEPASS_REDIRECT_URL `constant (i.e. `adobepass://ios.app`).

In the end the AccessEnabler will call the [`setAuthenticationStatus()`](#setAuthNStatus) callback with a status code of 0, indicating success of the logout flow.

  **Note:** If the user is logged in using Apple SSO the VSA203 status will be triggered. If this is the case, the user should be instructed to also logout from the system settings. Failure to do so will result in a re-authentication when the application is re-launched.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: initiate the logout flow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[Back to top...](#apis)

</br>

### getSelectedProvider {#getSelProv}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Use this method to determine the currently selected provider.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: determine the currently selected MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters:** None

**Callbacks triggered:** [`selectedProvider:`](#selProv)  

[Back to top...](#apis)

</br>

### selectedProvider {#selProv}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler that delivers information about the currently selected MVPD to the application.  

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: information about the currently selected MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters**:

* *mvpd*: object containing information about the currently selected MVPD  

**Triggered by:** [`getSelectedProvider`](#getSelProv)  

[Back to top...](#apis)

</br>

### getMetadata: {#getMeta}

**File:** AccessEnabler/headers/AccessEnabler.h

**Description:** Use this method to retrieve information exposed as metadata by the AccessEnabler library. The application can access this data by providing a dictionary-based *key* input parameter.

There are two types of metadata available to Programmers:

* Static metadata (Authentication token TTL, Authorization token TTL and Device ID) 
* User metadata (User-specific information, such as User ID, zip code; can be passed from an MVPD to a user's device during the Authentication and Authorization flows)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API call: query the AccessEnabler for metadata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters:**

* *keyDictionary*: a dictionary data structure, with the following
  format:
    * If key is `METADATA_OPCODE_KEY` and value is `METADATA_AUTHENTICATION`, then the query is made to obtain the authentication token expiration time.
    * If key is `METADATA_OPCODE_KEY` and value is `METADATA_AUTHORIZATION` **and**  
      key is `METADATA_RESOURCE_ID_KEY` and value is a particular resource ID, then the query is made to obtain the expiration time of the authorization token associated to the specified resource.
    * If key is `METADATA_OPCODE_KEY` and value is `METADATA_DEVICE_ID`, then the query is made to obtain the current device id. Note that this feature is disabled by default and Programmers should contact Adobe for information regarding enablement and fees.
    * If key is `METADATA_OPCODE_KEY` and value is `METADATA_USER_META` **and** key is `METADATA_USER_META_KEY` and value is the name of the metadata, then the query is made for user metadata. The list of available user metadata types:
        * `zip` - List of Zip Codes
        * `householdID` - Household identifier. In the case when an MVPD does not support subaccounts this will be identical to `userID`.      
        * `maxRating` - A collection of maximum parental ratings for the user      
        * `userID` - The user identifier. If an MVPD supports subaccounts, and the user is not the main account, `userID` will be different than `householdID.`     
        * `channelID` - A list of channels a user is entitled to view.

  >[!NOTE]
  >
  >The actual User Metadata available to a Programmer depends on what an MVPD makes available. This list will be expanded as new metadata is made available and added into the Adobe Pass Authentication system.

**Callbacks triggered:** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**More Information:** [User Metadata](/help/authentication/user-metadata.md)

[Back to top...](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler after calling[getAuthentication()](#getAuthN) if the current requestor supports at least one MVPD with SSO support.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: result of SSO flows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v2.0+

**Parameters**:

* viewController: represents the Apple SSO Dialog. This viewController needs to be displayed on the screen.

**Triggered by:** [`getAuthentication`](#getAuthN)

**More Information:** [iOS/tvOS Single Sign On](#presentTvDialog)

[Back to top...](#apis)

</br>

### dismissTVProviderDialog {#dismissTvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler after the user closes the Apple SSO Dialog.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: result of SSO flows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v2.0+

**Parameters**:

* viewController: represents the Apple SSO Dialog. This viewController needs to be removed from the screen.

**Triggered by:** User action

**More Information:** [iOS/tvOS Single Sign On](#presentTvDialog)

[Back to top...](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**File:** AccessEnabler/headers/EntitlementDelegate.h  

**Description** Callback triggered by the AccessEnabler that delivers the metadata requested via a [`getMetadata:`](#getMeta) call.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: result of metadata retrieval request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**Availability:** v1.0+

**Parameters**:

* *metadata*: The requested metadata. This value is an `NSString` in the case of static metadata (Authentication TTL, Authorization TTL, Device ID).  It is a complex object when requesting user specific metadata. This complex object is usually the Objective-C representation of a JSON payload (e.g. '{"street": "Main Avenue", "buildings": ["150", "320"]}' is translated in Objective-C as NSDictionary("street" -> "Main Avenue", "buildings" -> NSArray("150", "320"))).   Sample metadata JSON object:

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
```

* *encrypted*: Boolean value that specifies if the retrieved metadata is encrypted or not. This parameter is significant only for User Metadata requests, it has no meaning for Static Metadata (e.g., Authentication TTL) that is always received unencrypted. If this parameter is set to true, then it's up to the Programmer to obtain the unencrypted User Metadata value by performing an RSA decryption using the whitelisting private key (the same private key that is used for the signing of the Requestor ID in the [`setRequestor:setSignedRequestorId:`](#setReq) and `setRequestor:setSignedRequestorId:serviceProviders: `calls).

* *key*: The key used to formulate the metadata retrieval request.

* *arguments*: The same dictionary that was passed to the [`getMetadata:`](#getMeta) call. This is provided to allow the application to match the requests with the responses.

**Triggered by:** [`getMetadata:`](#getMeta)

**More Information:** [User Metadata](/help/authentication/user-metadata.md)


[Back to top...](#apis)

</br>

### MVPD {#mvpd}

**File:** AccessEnabler/headers/model/MVPD.h  

**Description** Describes the MVPD object. Can be used to obtain information about the MVPD's properties.

**Availability:** v1.0+ [boardingStatus property is available from v2.2] 

**Properties**:

* (NSString) ID - The MVPD Id.
* (NSString) displayName - The MVPD name. [This should be used to display in the picker]
* (NSString) logoURL - The MVPD logo address.
* (BOOL) enablePlatformServices - If true, the MVPD supports SSO services like [Apple SSO](#presentTvDialog).
* (NSString) boardingStatus - Can have 3 values:
    * nil - The MVPD does not support Apple SSO.
    * PICKER - The MVPD can appear in Apple picker but the authentication flow is done by Adobe.
    * SUPPORTED - The MVPD is fully supported by Apple and will use Apple's SSO token.

[Back to top...](#apis)

</br>

## Tracking Events {#tracking}

The AccessEnabler triggers an additional callback that is not necessarily related to the entitlement flows. Implementing the [`sendTrackingData()`](#sendTracking) callback function is optional, but it enables the application to track specific events and compile statistics such as number of successful/failed authentication/authorization attempts. 

### sendTrackingData:forEventType: {#sendTracking}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Description** Callback triggered by the AccessEnabler signaling to the application the occurrence of various events such as the completion/failure of authentication/authorization flows. With Adobe Pass Authentication 1.6, the device type, AccessEnabler client type, and operating system are reported by [`sendTrackingData()`](#sendTracking). The [`sendTrackingData()`](#sendTracking) callback remains backwards compatible.

**Callback: tracking events**

```
(void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event;
```

**Availability:** v1.0+

  **Note:** The device type and operating system are derived through the use of a public Java library (<http://java.net/projects/user-agent-utils>) and the user agent string. Be advised that this information is provided only as a coarse way to break down operational metrics into device categories, but that Adobe can take no responsibility for incorrect results. Please use the new functionality accordingly.

* Possible values for device type:
    * `computer`
    * `tablet`
    * `mobile`
    * `gameconsole`
    * `unknown`

* Possible values for AccessEnabler client type:
    * `flash`
    * `html5`
    * `ios`
    * `android`

  
**Parameters**:

* *event*: the code of the event that is being tracked. There are three possible tracking events types:
    * **authorizationDetection:** any time an authorization token request returns (event is `TRACKING_AUTHORIZATION`)
    * **authenticationDetection:** any time an authentication check occurs (event is `TRACKING_AUTHENTICATION`)
    * **mvpdSelection:** when the user selects an MVPD in the MVPD selection form (event is `TRACKING_GET_SELECTED_PROVIDER`)
* *data*: additional data that is associated to the reported event. This data is presented in the form of an list of values.

**Triggered by:** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

Instructions for interpreting the values in the *data* array:

* For trackingEventType `TRACKING_AUTHENTICATION:`
    * **0** - Whether the token request was successful (true/false) and if successful:
    * **1** - MVPD ID string
    * **2** - GUID (md5 hashed)
    * **3** - Token already in cache (true/false)
    * **4** - Device type
    * **5** - AccessEnabler client type
    * **6** - Operating system type

* For trackingEventType `TRACKING_AUTHORIZATION:`
    * **0** - Whether the token request was successful (true/false) and if successful:
    * **1** - MVPD ID
    * **2** - GUID (md5 hashed)
    * **3** - Token already in cache (true/false)
    * **4** - Error
    * **5** - Details
    * **6** - Device type
    * **7** - AccessEnabler client type
    * **8** - Operating system type
* For trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
    * **0** - ID of the currently selected MVPD
    * **1** - Device type
    * **2** - AccessEnabler client type
    * **3** - Operating system type

</br>
