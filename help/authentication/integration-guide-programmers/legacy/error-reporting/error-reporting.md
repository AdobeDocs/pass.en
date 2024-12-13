---
title: Error Reporting
description: Error Reporting
exl-id: a52bd2cf-c712-40a2-a25e-7d9560b46ba6
---
# (Legacy) Error Reporting {#error-reporting}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Overview {#overview}

Error reporting in Adobe Pass Authentication is currently implemented in two different ways:

*   **Advanced Error Reporting** The implementor registers an error callback in case of the [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) or implements an Interface method named "`status`" in case of the [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) and [AccessEnabler Android SDK](#accessenabler-android-sdk), in order to receive advanced error reporting. Errors are categorized into **Information**, **Warning**, and **Error** types. This reporting system is **asynchronous**, in that **there is no guarantee of the order in which multiple errors will be triggered**.  For details on the advanced error reporting system, see [Advanced Error Reporting](#advanced-error-reporting) section.

*   **Original Error Reporting -** A static reporting system in which error messages are passed to specific callback functions when specific requests fail. Errors are grouped into generic, authentication, and authorization types. For the list of error reported on in the original system, see the [Original Error Reporting](#original-error-reporting) section.


## Advanced Error Reporting {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT] 
>
>The old [Original Error Reporting](#original-error-reporting) API will continue to work as it did before, the advanced error reporting does not break the functionality, but the original error reporting will NOT receive any updates anymore. All new errors and updates will happen to the advanced error reporting system.

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

The new error reporting system is left optional, therefore the implementor can explicitly register an error handler callback to receive advanced error reports. The system includes the ability to register and unregister multiple error callbacks dynamically. In addition, you can register any new error callbacks as soon as the AccessEnabler JavaScript SDK is loaded, without the need to perform any other initialization (before calling `setRequestor()`), meaning that you have the ability to receive advanced reports on initialization and configuration errors.


#### Implementation {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


Your error handler callback function will receive a single object (a map) with the following structure:

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```    

### 1. Bind {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Attaches a handler for an event.

**`eventType`** - ONLY the "`errorEvent`" value results in the AccessEnabler JavaScript SDK triggering advanced error reports callbacks.

**`handlerName`** - a string specifying the name of the errors handler function.  
 

Both bind parameters must use only characters from the following set: `[0-9a-zA-Z][-._a-zA-Z0-9]`; that is, parameters must start with a number or letter, and can then include only hyphens, periods, underscores, and alpha-numeric characters.  In addition, parameters cannot exceed 1024 characters.  

**Example** of binding error handlers:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

Due to technical limitations you cannot bind a closure or an anonymous function. You must specify the name of the method in the second parameter.

 
### 2. Unbind {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Removes a previously-attached event handler.

**`eventType`** - ONLY the '`errorEvent`' value results in the AccessEnabler JavaScript SDK triggering advanced error reports callbacks.

**`handlerName`** - a string specifying the name of the errors handler function, if is null or missing all attached handlers for the specified `eventType` will be removed.

Both bind parameters must use only characters from the following set: `[0-9a-zA-Z][-._a-zA-Z0-9]`; that is, parameters must start with a number or letter, and can then include only hyphens, periods, underscores, and alpha-numeric characters.  In addition, parameters cannot exceed 1024 characters.  

**Example** of removing a single error handler:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Example** removing all error handlers:

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

The new error reporting system is mandatory, therefore the implementor must explicitly conform to the new Objective C "EntitlementStatus" protocol. This new approach allows programmers to receive advanced error reporting.

#### Implementation {#accessenab-ios-tvossdk-imp}

An implementor needs to conform to the following **EntitlementStatus** protocol:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Your **status** function will receive a single object (an `NSDictionary`) with the following structure:

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. Declaration**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. Implementation**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

The new error reporting system is mandatory, because the implementor must explicitly conform to the `IAccessEnablerDelegate` interface defined protocol. This new approach allows programmers to receive advanced error reporting.

#### Implementation {#access-enablr-androidsdk-imp}

An implementor needs to handle the new `status` method from the interface`IAccessEnablerDelegate`. The **`status`** function will receive a single **`AdvancedStatus`** object having the following model:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Sample**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


The new error reporting system is mandatory, because the implementor must explicitly conform to the `IAccessEnablerDelegate` interface defined protocol. This new approach allows programmers to receive advanced error reporting.

#### Implementation {#access-enab-fireos-sdk-}

An implementor needs to handle the new `status`method from the interface`IAccessEnablerDelegate`. The **`status`** function will receive a single **`AdvancedStatus`** object having the following model:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Sample**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## Advanced Error Codes Reference {#advanced-error-codes-reference}

The following table lists and describes the error codes exposed by the newer error API, along with suggested actions to be taken to correct them:

|ID|Level|Description|Developer Actions|User Actions|JavaScrip|iOS/tvOS|Android|
|---|-------------|------------|----------------|---|---|---|---|
AAPL& AAPL_ERROR |Error | Generic Apple SSO error |    The error contains a details field with the original VSA error. | n/a |    n/a |    Yes |    n/a
|VSA203 | Info |The user decided to log out of the application while the authentication happened as a result of a sign-in through the platform SSO. | Instruct/prompt the user to explicitly sign out from Settings -> Accounts -> TV Provider on tvOS. <br><br> Instruct/prompt the user to explicitly sign out from Settings -> TV Provider on iOS/iPadOS.| Explicitly sign out from Settings -> Accounts -> TV Provider on tvOS. <br> <br> Explicitly sign out from Settings -> TV Provider on iOS/iPadOS | n/a |  Yes | n/a |
|VSA404| Info | Application Video Subscriber Account permission is undetermined. | Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. | The user can change its decision by going to the application settings (TV Provider access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.     | n/a |    Yes    |n/a| 
|VSA503 | Info | Application Video Subscriber Account metadata request failed. | The MVPD endpoint is not responding. The application could fallback to regular authentication flow. | n/a |    n/a |    Yes | n/a| 
| 500 |    Error | Internal error | Use AccessEnablerDebug and inspect debug logs (console.log output) in order to determine what went wrong. |    n/a     |Yes |    Yes |    n/a| 
| SEC403 | Error | Domain Security error. The requestor is using an invalid domain. All domains used by a particular Requestor ID need to be whitelisted by Adobe. | - Load the AccessEnabler only from the list of allowed domains <br> <br> - Contact Adobe in order to manage the domain whitelist for the Requestor ID used <br> <br> - iOS: verify that you are using the correct certificate and that the signature is created properly | n/a |n/a |    Yes | n/a | 
|SEC412 | Warning | [ Available in Release 2.5 ] Device ID does not match. This can happen whenever the underlying platform changes its Device ID. In this case the existing tokens will be cleared and the user will not be authenticated anymore. Note that this is happening legitimately when the user is using the JS SDK and is roaming (on JS the client IP is part of the Device ID). Otherwise this could be an indication of a fraud attempt - an attempt to copy tokens from a different device. | - Monitor the number of warnings. If they spike for no apparent reason (no recent browser updates; new operating systems) that might be an indicator of fraud attempts.  <br> <br>- Optionally, inform the user that he needs to log in again. |Login again.| Yes | Yes | Yes from 3.2| 
|SEC420| Error| HTTP Security error when communicating with Adobe Pass Authentication servers. This error typically occurs when spoofing / proxies are in place.| - Load `[https://]{SP_FQDN\}` in the browser and manually accept the SSL certificates, for example, **https://api.auth.adobe.com** or **https://api.auth-staging.adobe.com** <br> <br>- Mark the proxy certs as trusted | If this occurs for a regular user, it is an indication of a possible man-in-the-middle attack! | Yes | Yes | Yes from 3.2 | 
|CFG100| Warning | The client machine Date / Time / Timezone is not set correctly. This will likely lead to authentication / authorization errors. | - Inform the user to set the correct time. <br> <br> Take actions to prevent entitlement flows, since they will likely fail. | Set the correct Date / Time. | Yes | Yes | Yes from 3.2 | 
| CFG400 |     Error | An invalid Requestor ID was supplied. |    The developer MUST specify a valid Requestor ID. |    n/a |    Yes |    Yes | Yes from 3.2 | 
| CFG404 |    Error |    The Adobe Pass Authentication servers were not found. This can happen in 3 instances: <br><br> - The developer has an invalid spoofing in place. <br><br> -The user has networking issues and cannot reach the Adobe Pass Authentication domains. <br><br> -Adobe Pass Authentication servers are misconfigured. <br><br>  **Note:** On Firefox, CFG400 will appear instead of CFG404 (browser limitation) | - Check spoofing. <br><br> -Check network / DNS settings. <br><br> -Inform Adobe. | Check network / DNS settings.  | Yes  |Yes | Yes from 3.2 | 
|CFG410| Error | AccessEnabler is too old.| Inform the user to clear caches. | Clear the browser cache. | Yes |     n/a |     Yes from 3.2|
|CFG5xx| Error| The Adobe Pass Authentication servers are experiencing internal errors. xx can be any number. | - Inform the user of Adobe Pass Authentication unavailability. <br><br> - Bypass Adobe Pass Authentication. <br> <br> - Inform Adobe. | Try later. |    Yes |    Yes | Yes from 3.2 | 
| N000 |    Info |    The user is not authenticated. |    n/a |    Login. |Yes| Yes| Yes from 3.2 | 
| N001 |Info| A passive authentication attempt was started in the background. This will happen for MVPDs configured with "Authentication Per Requestor". While the user will hopefully be automatically authenticated, this incurs a performance penalty on initialization.|    Optionally inform the user, or present UI that alerts the user, that "work is in progress". |    Wait. |     Yes | Yes | Yes from 3.2 | 
|N003 |    Info |    The user selects the "Other TV Provider" option from Apple MVPD picker. |The *displayProviderDialog* callback will be called and the application could fallback to regular authentication flow. |     Select regular MVPD and continue with the login screen. |    n/a |    Yes |    n/a|
|N004|     Info |    The user selects a TV Provider which is not supported by the current requestor. |The *displayProviderDialog* callback will be called and the application could fallback to regular authentication flow. |    Select regular MVPD and continue with the login screen. |    n/a |    Yes |n/a|
|N005| Info | The MVPD picker was cancelled. |n/a |    n/a |    Yes |    Yes | Yes from 3.2 |
|N010 |    Warning | The user was authenticated while the authenticate-all degradation rule was in place for the selected MVPD. | Optionally inform the user that he is getting "complimentary" free access due to MVPD difficulties. | n/a | Yes | Yes | Yes from 3.2 | 
|N011|     Info |    The user was authenticated using TempPass. | - Inform the user. <br> <br> - Optionally present a list of regular MVPDs. |  Optionally login with your regular MVPD. | Yes | Yes |    Yes from 3.2 | 
|N111| Warning | Expired TempPass.| - Inform user. <br> <br> - Present a list of regular MVPDs. <br> <br> - Hide the TempPass option. | Login with your regular MVPD. | Yes | Yes | Yes from 3.2 |
|N130| Error | **Authentication token not found on session.**  This may be due to one of the following: <br> <br> 1. Browser has (3rd-party) cookies disabled (Not applicable for AccessEnabler JavaScript SDK version 4.x) <br> <br> 2. Browser has Prevent cross-site tracking enabled (Safari 11+) <br> <br> 3. Session has expired <br> <br> 4. Programmer calls authentication APIs in incorrect succession <br> <br> NOTE: This error code is not available for full-page redirect authentication flows. | 1. Prompt user to enable (3-rd party) cookies <br> <br> 2. Promt user to disable cross-site tracking <br> <br> 3. Prompt user to re-authenticate <br> <br> 4. Call APIs in correct order | 1. Enable (3-rd party) cookies <br> <br> 2. Disable cross-site tracking <br> <br> 3. Re-authenticate <br> <br> 4. N/A | Yes | Yes | Yes from 3.2|
|N500| Error| Internal error. <br> <br> Note: This is the original error system's "Generic Authentication Error" and "Internal Authentication Error". This error will eventually be phased out. | Use AccessEnablerDebug  and inspect debug logs (console.log output) in order to determine what went wrong. |  n/a |     Yes |    Yes |     n/a |
|R401 | Error |    There was an error while trying to obtain an access token. <br> <br> Note: This is an unrecoverable error. Inform the user that the application is unavailable. | - iOS: Check the software statement and custom schemes in your application. <br> <br> - JavaScript: Check the software statement in your website application. <br> <br> Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v4.0 | Yes From v3.0 | Yes from 3.2 | 
|R400 | Error | Application is not registered. The software statement is invalid or it has been revoked. <br> <br> Note: This is an unrecoverable error. Inform the user that the application is unavailable. | - iOS: Check the software statement and custom schemes in your application. <br> <br> - JavaScript: Check the software statement in your website application. <br> <br> Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v4.0 | Yes From v3.0 | Yes from 3.2 |
|REG500| Error | Registration code could not be fetched from server. <br> <br> Note: This is an unrecoverable error. Inform the user that the application is unavailable.| Open a ticket using Zendesk and inform the user that the system is temporarily unavailable. | n/a     | Yes From v4.0 | Yes From v3.0 |Yes from 3.2 |
|REGCODE|     Success | The application called setSelectedProvider API on tvOS platform. | Instruct/prompt the user to use a 2nd device (screen) to login using the provided registration code. |    Use the regcode on a 2nd device (screen) to initiate authentication.|  n/a | Yes Only for tvOS |n/a|
|Z010|     Warning| The user was authorized while the authenticate-all or authorize-all degradation rule was in place for the selected MVPD. | Optionally inform the user that he is getting "complimentary" free access due to MVPD difficulties. | n/a | Yes| Yes| Yes from 3.2 | 
|Z011 |    Info |    User was authorized using TempPass | Optionally inform the user | n/a | Yes | Yes | Yes from 3.2 |
|Z100 |    Error |    Authorization failed because the user has no subscription for the requested resource or because of other reasons originating from the MVPD, e.g. the video does not match the Parental Control settings for the user account | - Do not allow playback. <br> <br> - Inform the user. <br> <br> - The 'message' key in the error message MAY contain a more detailed message supplied by the MVPD.| n/a | Yes | Yes | Yes from 3.2 | 
|Z110 |    Error |    Authorization denied due to repeated MVPD denials. Possible fraud attempt or DOS. | - Do not allow playback. <br> <br> - Inform the user. | n/a  | Yes | Yes  |    Yes from 3.2|
|Z120 |    Error |    Authorization denied due to technical reasons in communicating with the MVPD. Possible network error. | - Do not allow playback. <br> <br> - Inform the user that the MVPD experienced difficulties and they should try later. | Try later. |    Yes |    Yes | Yes from 3.2 | 
|Z130 | Error | Authorization denied because an invalid / malformed resource was used.|Check the resource string and correct it. Generally this error is due to either a malformed MRSS or using a plain string instead of MRSS. | n/a | Yes | Yes | Yes from 3.2 |
|Z169 |    Error |    Authorization denied because authzNone degradation rule has been applied for the specified resource. | Inform the user | n/a | Yes | Yes |Yes from 3.2 |
|Z500 | Error | Internal error. <br> <br>  Note: this is the legacy "Generic Authentication Error" and "Internal Authentication Error". This error will eventually be phased out. | Use AccessEnablerDebug  and inspect debug logs (console.log output) in order to determine what went wrong. |    n/a | Yes| Yes |Yes from 3.2 |
|P100 |    Error |    Preauthorization failed. Most likely this is due to requesting authorization for too many resources.  | - Do NOT use more than the maximum number of allowed resources. <br> <br> -  Contact Adobe Pass Authentication support to find / set up the maximum number of allowed resources. | n/a | Yes From v3.0 | Yes | Yes from 3.2 | 
|IS2XX | Error | These error codes are returned when the individualization server endpoint response data has an invalid format or is missing required individualization information. | Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v3.0 | n/a |    n/a |
|IS4XX| Error | These error codes are returned in case of individualization server endpoint failure 4XX - is the HTTP status code of the response. | Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v3.0 | n/a | n/a | 
|IS5XX | Error | These error codes are returned in case of individualization server endpoint failure 5XX - is the HTTP status code of the response. | Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v3.0 | n/a |    n/a | 
|IS0 |     Error |    This code is returned when the individualization server endpoint did not respond at all, therefore the connection has timed out  |    Open a ticket using Zendesk and inform the user that the system is temporarily unavailable | n/a | Yes From v3.0 | n/a | n/a | 
|LS011 | Warning | AccessEnabler is using a volatile storage because due to LSO / LocalStorage problems and WebStorage issues (or unavailability). <br> <br> Authentication / authorization does not persist beyond current page!. Each page load will result in the user needing to authenticate. Configured TTLs are not enforced across page reloads. | - Inform the user of limitations. <br> <br> - Inform the user how to increase available storage space. <br> <br> - Alternatively logout in order to clear the storage. | - Increase storage. <br> <br> - Logout in order to clear storage. | Yes | n/a | n/a | 

<br>

## Original Error Reporting {#original-error-reporting}

This section describes the original error reporting system, along with the original error codes. In the original error reporting system, the AccessEnabler passes errors to these two callback functions: `setAuthenticationStatus()` after a call to `checkAuthentication()`; `tokenRequestFailed()`, after the failure of a call to `checkAuthorization()` or `getAuthorization()`.

The original error reporting and status API's continue to work exactly as before. However, going forward the original error reporting API's will not be updated. All new error reporting and updates on the old errors will be reflected ONLY in the newe [Advanced Error Reporting system](#advanced-error-reporting).


For examples of using the original error reporting system, see the [JavaScript API Reference](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) and [tokenRequestFailed()](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#token-request-failed-error-msg) functions, [iOS/tvOS API Reference](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#setAuthNStatus)and [tokentRequestFailed()](/help/authentication/integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md#tokenReqFailed), [Android API Reference](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#setAuthNStatus) and [tokenRequestFailed()](/help/authentication/integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Original Callback Error Codes {#original-callback-error-codes}

|**Generic Errors** | | 
|---|---|
|Internal Error | A system error occurred when trying to process request.|
|Provider not Selected Error |    Occurs when customer cancels in the provider selection dialog.|
|Provider not Available Error |    Occurs when no providers are available.|
|||
|**Authentication Errors** | |
|Generic Authentication Error |     Returned when the reason is not known or cannot be published.|
|Internal Authentication Error |    A system error occurred when trying to authenticate.|
|User Not Authenticated Error |    User is not authenticated.|
||| 
|**Authorization Errors**||
|Generic Authorization Error |     Returned when the reason is not known or cannot be published.|
|Internal Authorization Error |    A system error occurred when trying to authorize.|
|User not Authorized Error |     The customer is not authorized to view the requested content.|

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
