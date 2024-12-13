---
title: Android SDK with Dynamic Client Registration
description: Android SDK with Dynamic Client Registration
exl-id: 8d0c1507-8e80-40a4-8698-fb795240f618
---
# (Legacy) Android SDK with Dynamic Client Registration {#android-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Intro}

Android AccessEnabler SDK for Android was modified to enable Authentication without using session cookies. As more and more browsers are restricting the access to cookies, another method needs to be used to allow authentication.

For Android, the usage of Chrome Custom Tabs restricts the access to cookies from other applications.

>**Android SDK 3.0.0** introduces:

- dynamic client registration replaces the current app registration mechanism based on signed requestor ID & session cookie authentication
- Chrome Custom Tabs for authentication flows

>[!NOTE]
>
>For older Android versions without Chrome Custom Tabs support will use the WebView authentication similar as in older AccessEnabler SDK versions.


## Dynamic Client Registration {#DCR}

Android SDK v3.0+ will use the Dynamic Client Registration procedure as defined in [Dynamic Client Registration Overview](../../../rest-apis/rest-api-dcr/dynamic-client-registration-overview.md).


## Feature demo {#Demo}

Please watch [this webinar](https://my.adobeconnect.com/pzkp8ujrigg1/) which gives more context of the feature and contains a demo on how to manage the software statements using the TVE Dashboard and how to test the generated ones using a demo application provided by Adobe as part of Android SDK.

## API Changes {#API}


### Factory.getInstance

**Description:** Instantiates the Access Enabler object. There should be a single Access Enabler instance per application instance.

| API call: constructor |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException |


**Availability:** v3.0+

**Parameters:**

- *appContext*: Android application context
- softwareStatement: value obtained from TVE Dashboard or *null* if "software\_statement" is set in strings.xml
- redirectUrl : unique url, one of the domains in reverse order that was explicitly added in TVE Dashboard or *null* if "redirect\_uri" is set in strings.xml

Note : invalid softwareStatement or redirectUrl will cause the application not to initialize AccessEnabler or to register application for Adobe Pass Authentication and authorization
</br>
Note : redirectUrl parameter or redirect\_uri in strings.xml should be the value of the domain added in TVE Dashboard for the application in reverse order ( for ex : for domain 'adobe.com' added in TVE Dashboard, the redirectUrl should be 'com.adobe'.
 

### setRequestor

**Description:** Establishes the identity of the Channel. Each Channel is assigned a unique ID upon registering with Adobe for the Adobe Pass Authentication system. When dealing with SSO and remote tokens the authentication state can change when the application is in the background, setRequestor can be called again when the application is brought into foreground in order to synchronize with the system state (fetch a remote token if SSO is enabled or delete the local token if a logout happened in the meantime).

The server response contains a list of MVPDs together with some configuration information that is attached to the identity of the Channel. The server response is used internally by the Access Enabler code. Only the status of the operation (i.e. SUCCESS/FAIL) is presented to your application via the setRequestorComplete() callback.

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

- *requestorID*: The unique ID associated with the Channel. Pass the unique ID assigned by Adobe to your site when you first registered with the Adobe Pass Authentication service.
- *urls*: Optional parameter; by default, the Adobe service provider is used [http://sp.auth.adobe.com/](http://sp.auth.adobe.com/). This array allows you to specify endpoints for authentication and authorization services provided by Adobe (different instances might be used for debugging purposes). You can use this to specify multiple Adobe Pass Authentication service provider instances. When doing so, the MVPD list is composed of the endpoints from all the service providers. Each MVPD is associated with the fastest service provider; that is, the provider that responded first and that supports that MVPD.

Deprecated:

- *signedRequestorID*: A copy of the requestor ID that is digitally signed with your private key. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Callbacks triggered:** `setRequestorComplete()`

### logout

**Description:** Use this method to initiate the logout flow. The logout is the result of a series of HTTP-redirect operations due to the fact that the user needs to be logged out from both Adobe Pass Authentication servers and also from the MVPD's servers. As a result, this flow will open a ChromeCustomTab window to execute logout.

| API call: initiate the logout flow |
| --- |
| public void logout() |

**Availability:** v3.0+

**Parameters:** None
  
**Callbacks triggered:** `setAuthenticationStatus()`
</br></br>

## Programmer Implementation Flow {#Progr}

### **1. Register Application** 

a. Obtain software\_statement and redirect\_uri from Adobe Pass ( TVE Dashboard )

b. There are two options to pass these values to Adobe Pass SDK :

In strings.xml add : 

```XML
<string name="software_statement">[softwarestatement value]</string>
<string name="redirect_uri">application_url.com</string>
```

Call AccessEnabler.getInstance(appContext,softwareStatement,
redirectUrl)


### 2. Configure Application

a. setRequestor(requestor\_id) 

  SDK will do the following operations: 

- register application: using **software\_statement**, SDK will obtain a **client\_id, client\_secret, client\_id\_issued\_at, redirect\_uris, grant\_types**. This information will be stored in the application's internal storage.

- obtain an **access\_token** using client\_id, client\_secret and grant\_type="client\_credentials" . This access\_token will be used on each call made by the SDK to Adobe Pass servers 

**Token Error Responses :**

| Error responses | | |
| --- | --- | --- |
| HTTP 400 (Bad Request) | {"error": "invalid\_request"}     | The request is missing a required parameter, includes an unsupported parameter value (other than grant type), repeats a parameter, includes multiple credentials, utilizes more than one mechanism for authenticating the client, or is otherwise malformed. |
| HTTP 400 (Bad Request) | {"error": "invalid\_client"}      | Client authentication failed because the client was unknown. The SDK MUST register with the authorization server again. |
| HTTP 400 (Bad Request) | {"error": "unauthorized\_client"} | The authenticated client is not authorized to use this authorization grant type. |

- in case an MVPD requires Passive Authentication, a Chrome Custom Tab will open to execute passive with that MVPD and will close when complete

b. checkAuthentication()

- true : go to Authorization
- false : go to Select MVPD

c. getAuthentication : SDK will include **access_token** in call parameters 

- mvpd remembered : go to setSelectedProvider(mvpd_id)
- mvpd not selected : displayProviderDialog
- mvpd selected : go to setSelectedProvider(mvpd_id)

d. setSelectedProvider

- mvpd\_id authentication url is loaded in ChromeCustomTabs
- login successful : delegate.setAuthenticationStatus ( SUCCESS )
- login canceled : reset MVPD selection
- URL scheme is established as "adobepass://redirect_uri" to capture when the authentication is complete

e. get/checkAuthorization : SDK will include **access_token** in header as Authorization: Bearer **access_token**

- if authorization is succesful, a call will be made for obtaining the
media token

f. logout : 

- SDK will delete valid token for the current requestor (authentications obtained by other applications and not through SSO will remain valid)
- SDK will open Chrome Custom Tabs to reach mvpd_id logout endpoint. Once completed, the Chrome Custom Tabs will be closed
- URL scheme is established as "adobepass://logout" to capture the moment when logout is complete
- logout will trigger a sendTrackingData(new Event(EVENT_LOGOUT,USER_NOT_AUTHENTICATED_ERROR) and a callback : setAuthenticationStatus(0,"Logout")

**Note:** as each call requires an **access_token,** possible error codes below are handled in the SDK. 


| Error responses | | |
| --- | ---|--- |
| invalid_request | 400 | The request is malformed. The SDK should stop performing calls to the server. |
| invalid_client | 403 | The client id is not longer permitted to perform requests. The sdk MUST perform again the client registration.|
| access_denied | 401 | The access\_token is not valid. The sdk MUST request a new access_token. |
