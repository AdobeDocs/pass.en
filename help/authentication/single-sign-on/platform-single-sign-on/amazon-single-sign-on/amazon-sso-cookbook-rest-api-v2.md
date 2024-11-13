---
title: Amazon SSO Cookbook (REST API V2)
description: Amazon SSO Cookbook (REST API V2)
exl-id: 44365f9b-a8d0-4991-8e4a-7b15eabcbd30
---
# Amazon SSO Cookbook (REST API V2) {#amazon-sso-cookbook-rest-api-v2}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The Adobe Pass Authentication REST API V2 has support for Platform Single Sign-On (SSO) for end users of client applications running on FireOS.

This document acts as an extension to the existing [REST API V2 Overview](/help/authentication/rest-api-v2/rest-api-v2-overview.md) that provides a high-level view and the document that describes how to implement [Single sign-on using platform identity flows](/help/authentication/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md).

## Amazon single sign-on using platform identity flows {#cookbook}

### Prerequisites {#prerequisites}

Before proceeding with the Amazon single sign-on using platform identity flows, ensure the following prerequisites are met.

#### Integrate Amazon SSO SDK {#integrate-amazon-sso-sdk}

The streaming application must integrate the [Amazon SSO SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) library for Single Sign-On (SSO) into its build.

  * Download and copy the latest Amazon SSO SDK library into a `/SSOEnabler` folder parallel to the application's directory.

  * Update the manifest and Gradle files to use the Amazon SSO SDK library.

    **Manifest:**

    ```JAVA
    <uses-library android:name="com.amazon.ottssotokenlib" android:required="false">
    ```

    **Gradle:**

    Under repositories:

    ```JAVA
    flatDir {
        dirs '../SSOEnabler'
    }
    ```

    Under dependencies:
    
    ```JAVA
    provided fileTree(include: ['ottSSOTokenStub.jar'], dir: '../SSOEnabler')
    ```

#### Use Amazon SSO SDK {#use-amazon-sso-sdk}

The streaming application must use the Amazon SSO SDK to obtain the SSO token (platform identity) payload.

The Amazon SSO SDK provides both synchronous and asynchronous APIs to obtain the SSO token (platform identity) payload.

The streaming application can choose one of the two options based on its architecture.

##### Asynchronous APIs

* Get the `SSOEnabler` instance and set the `SSOEnablerCallback`:

  ```JAVA
  SSOEnabler ssoEnabler = SSOEnabler.getInstance(context);
  
  SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
  ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
  ```
  
  This can be done during the initialisation of the streaming application.

  ```JAVA
  public static abstract class SSOEnablerCallback
  {
          public abstract void getSSOTokenSuccess(Bundle result);
          public abstract void getSSOTokenFailure(Bundle result);
  }
  ```

  The SSO token success response bundle will contain:
    * An SSO token as a `string` with key "SSOToken".
  
  <br/>
  
  The SSO token failure response bundle will contain:
    * An error code as an `int` with key "ErrorCode".
    * An error description as a `string` with key "ErrorDescription".

  <br/>
  
* Get the SSO token:

  ```JAVA
  Bundle getSSOTokenAsync(Void);
  ```

  This API will provide the response via callback set during the initialisation.

##### Synchronous APIs

* Get the `SSOEnabler` instance:

  ```JAVA
  SSOEnabler ssoEnabler = SSOEnabler.getInstance(context);
  ```

* Get the SSO token:

  ```JAVA
  Bundle getSSOTokenSync(Void);
  ```

  This API will block the caller thread and respond with the result bundle. Since this is a synchronous call, be sure to not use it in your main thread.

  ```JAVA
  void setSSOTokenTimeout(long);
  ```

  This API will set the timeout value for the synchronous call. The default timeout value is 1 minute.

#### Fallback for Amazon SSO {#fallback-amazon-sso}

The streaming application must handle fallback scenarios from the Amazon SSO flow to the regular authentication flow.

Ensure that the streaming application is handling:

* The absence of the Amazon companion application that should be running on the Amazon device. 
  * The streaming application may encounter a `ClassNotFoundException` at runtime on the following class `com.amazon.ottssotokenlib.SSOEnabler`.

* The absence of the SSO token (platform identity) payload that should be returned by the above APIs.
  * The streaming application may contact the Amazon and Adobe representatives to investigate.

### Workflow {#workflow}

The Amazon SSO token (platform identity) payload needs to be present on all HTTP requests made against Adobe Pass Authentication REST API V2 endpoints:

```
/api/v2/*
```

Adobe Pass Authentication REST API V2 supports the following methods to receive the SSO token (platform identity) payload which is a device-scoped or platform-scoped identifier:

* As a header named: `Adobe-Subject-Token`

>[!IMPORTANT]
> 
> For more details about `Adobe-Subject-Token` header, refer to the [Adobe-Subject-Token](/help/authentication/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-adobe-subject-token.md) documentation.

#### Samples

**Sending as a header**

```HTTPS
GET /api/v2/{serviceProvider}/sessions HTTP/1.1 
Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

>[!IMPORTANT]
>
> In case the `Adobe-Subject-Token` header value is missing or invalid, then Adobe Pass Authentication will service the requests without taking Single Sign-On into account.
