---
title: JavaScript SDK Cookbook
description: JavaScript SDK Cookbook
exl-id: d57f7a4a-ac77-4f3c-8008-0cccf8839f7c
---
# JavaScript SDK Cookbook {#javascript-sdk-cookbook}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro}

This document describes the entitlement workflows that a Programmer's upper-level application implements for a JavaScript integration with Adobe Primetime Authentication service. Links to the JavaScript API Reference are included throughout.  

Also note that the [Related Information](#related) section includes a
link to a set of JavaScript code samples.

## Entitlement Flows {#entitlement}

1.  [Prerequisites](#prereq)
2.  [Startup Flow](#startup)
3.  [Authentication Flow](#authn)
4.  [Authorization Flow](#authz)
5.  [View Media Flow](#logout)

</br>

![](assets/javascript-flows.png)


## Prerequisites {#prereq}

**Dependencies:**

- Adobe Primetime authentication Library (AccessEnabler), work with your Adobe Primetime authentication Account Manager to arrange this.
- Valid Adobe Primetime authentication requestorId, work with your Adobe Primetime authentication Account Manager to arrange this.

Create your callback functions:

- `entitlementLoaded`
</br>
  
  **Trigger:** The AccessEnabler has loaded and finished initializing.

- `displayProviderDialog(mvpds)`

  **Trigger:** `getAuthentication(),` only if the user has not selected a provider (an MVPD), and is not yet authenticated
  The mvpds parameter is an array of providers available to the user.

- `setAuthenticationStatus(status, errorcode)`

  **Trigger:**
  - `checkAuthentication()`every time.
  - `getAuthentication()` only if the user is already authenticated and has selected a provider.
  
  Status returned is success or failure; the errorcode describes the type of the failure.

- `createIFrame(width, height)`
  
  **Trigger:** `setSelectedProvider(providerID)`, only if the selected provider is configured to display in an IFrame.

  >[!NOTE]
  >
  >A provider is configured to render its authentication screen as either a redirect or in an iFrame, and the Programmer needs to account for both.

- `sendTrackingData(event, data)`

  **Triggers:** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  The `event` parameter indicates which entitlement event occurred; the `data` parameter is a list of values relating to the event. 
- `setToken(token, resource)`
  **Trigger:** `checkAuthorization()`and `getAuthorization()` after a successful authorization to view a resource.   The `token` parameter is the short-lived media token; the `resource` parameter is the content that the user is authorized to view.

- `tokenRequestFailed(resource, code, description)`
  **Trigger:**`checkAuthorization()`and`getAuthorization()`  after an unsuccessful authorization.  
The `resource` parameter is the content that the user was attempting to view; the `code` parameter is the error code indicating what type of failure occurred; the `description` parameter describes the error associated with the error code.

- `selectedProvider(mvpd)`

  **Trigger:** [`getSelectedProvider()`](#$getSelProv The `mvpd` parameter provides information about the provider selected by
the user.

- `setMetadataStatus(metadata, key, arguments)`
  
  **Trigger:** `getMetadata().`  
The `metadata` parameter provides the specific data you requested; the key parameter is the key used in the `getMetadata()`request; and the `arguments` parameter is the same dictionary that was passed to `getMetadata()`.


## 2. Startup Flow

**I.  Load the AccessEnabler JavaScript:**
  
  **For Staging Profile**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"

```

or...

  **For Production Profile**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"

```  
  
**Triggers:** When initialization is complete, Adobe Primetime
authentication calls your `entitlementLoaded()` callback function. This is the entry point to your application's communication with the AccessEnabler. 

 
**II.** Call `setRequestor()`to establish the
identity of the Programmer; pass in the Programmer's `requestorID` and
(optionally) an array of Adobe Primetime authentication endpoints.

**Triggers:** None, but enables `displayProviderDialog()` to be called when needed.


**III.** Call `checkAuthentication()` to check for an existing authentication without initiating the full [authentication flow].  If this call succeeds, you can proceed directly to the `authorization flow`.  If not, proceed to the `authentication flow`.

**Dependency:** A successful call to `setRequestor()`(this dependency applies to all subsequent calls as well).

 **Triggers:** `setAuthenticationStatus()` callback

</br>

## 3. Authentication Flow</span>


**Dependency:** A successful call to `setRequestor()`(this dependency applies to all subsequent calls as well).


Call `getAuthentication()` to get the authentication status OR to trigger the provider authentication flow.

**Trigers:**

- `displayProviderDialog()`if the user has not yet been authenticated
- `setAuthenticationStatus()` if authentication already took place

The completion of the authentication flow is reached when the AccessEnabler calls `setAuthenticationStatus()`with `isAuthenticated == 1`.

## 4. Authorization Flow {#authz}

**Dependencies:**

- A successful call to `setRequestor()` (this dependency applies to all subsequent calls as well).
- Valid ResourceID(s) agreed upon with the MVPD(s). Note that ResourceIDs should be the same as those used on any other devices or platforms, and will be the same across MVPDs.

Call `getAuthorization()` and pass the ResourceID for the requested media. A successful call will return a Short Media Token, which confirms that the user is authorized to view the requested media.

- If the call passes: The user has a valid AuthN token and the user is authorized to watch the requested media.
- If the call fails: Examine the Exception thrown to determine its type (AuthN, AuthZ, or something else):
- If the call was an AuthN error then re-start the AuthN Flow.
- If the call was an AuthZ error then the user is not authorized to watch the requested media and some kind of error message should be displayed to the user.
- If there was some other error (connection error, network error, etc.) then display an appropriate error message to the user.

Use the Media Token Verifier to validate the shortMediaToken returned from a succesful `getAuthorization()` call.

 
**Dependency:** The Short Media Token Verifier (included with the
AccessEnabler library)

- If the validation passes: Display/Playback the requested media for the user.
- If it fails: The AuthZ token was invalid, the media request should be refused, and an error message should be displayed to the user.

## 5. View Media Flow {#logout}

- The user selects the media to view.
    - Is media protected?  
      - Your app checks if the media is protected:
        - If the media is protected, your app starts the Authorization (AuthZ) Flow above.
        - If the media is not protected, then proceed with the View Media flow.
        - Playback media

## Configuring the Visitor ID {#visitorID}

Configuring a [Experience Cloud visitorID](https://experienceleague.adobe.com/docs/id-service/using/home.html) value is very important from the analytics point of view. Once a EC visitorID value is set, the SDK will send this information along with every network call and the Adobe Primetime Authentication service will collect this information. This way you will be able to correlate the analytics data from Adobe Primetime Authentication service with any other anayltics reports that you may have from other applications or websites. Information on how to setup EC visitorID can be found [here](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).

 
>[!NOTE]
>
>Note that this functionality support is available starting with JS SDK version 3.1.0. 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->
