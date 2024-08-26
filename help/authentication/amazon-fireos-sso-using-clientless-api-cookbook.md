---
title: Amazon FireOS SSO using Clientless API Cookbook
description: Amazon FireOS SSO using Clientless API Cookbook
exl-id: 4c65eae7-81c1-4926-9202-a36fd13af6ec
---
# Amazon FireOS SSO using Clientless API Cookbook {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Introduction {#Introduction}

This document provides instructions to implement Amazon's SSO version of Adobe Pass Authentication flow using clientless API. The first part of this document focuses on the specificity of Amazon version of the architecture, for the many partners already familiar and experienced with its implementation.

Second part of the document goes over the main steps to implement Adobe Pass Authentication clientless API.

For a broad technical overview of how the Clientless solution works, see the [REST API Overview](/help/authentication/rest-api-overview.md). Adobe is the preferred contact for support about the overall architecture and first implementations.

## Amazon Clientless SSO {#AMZ-Clientless-SSO}

### High Level Architecture {#High-Level-Arch}

The Amazon clientless SSO implementation is simple and mostly identical to the regular Adobe PrimeTime Authentication clientless APIs.

You will need to use Amazon SDK to retrieve a personalized payload and use it when calling Adobe clientless APIs.

If the payload is recognized and corresponds to an authenticated session, the clientless APIs will return right away with your session's token.

### How to build the application to use Amazon SDK {#Build-entries}

* Download and copy the latest [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) into a /SSOEnabler folder parallel to the app directory
* Update manifest/gradle files to use the library :

    **Add the following line to your Manifest file:**

    ```Java
    <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
    ```

    **Gradle file entries:**

    Under repositories:

    ```java
    flatDir {
         dirs '../SSOEnabler'
    }
    ```

    Under dependencies, add:
    
    ```Java
    provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
    ```


* Handling the absence of the Amazon companion app:

    While not likely, should the companion not be present on the Amazon device your application is running, you should encounter a ClassNotFoundException at runtime on the following class: `com.amazon.ottssotokenlib.SSOEnabler`.

    Should this happen, all you need to do is skip the payload step and fall back on the regular PrimeTime flow. SSO won't be enabled but regular auth flow will happen normally.

</br>

### How to obtain Amazon SSO payload using Amazon SDK {#UseAmazonSSO}

During your application initialization, obtain an instance of SSOEnabler. Based on your application architecture, you should decide between a synchronous or asynchronous implementation.

If for any reason, the API calls don't return a payload, please use the regular non-SSO flow and contact your Amazon and Adobe partners to investigate.

**Asynchronous API**

* Get SSO Enabler instance:

  ```Java
  ssoEnabler = SSOEnabler.getInstance(context);
  SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
  ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
  ```


* Set the callback 

  ```java
  public static abstract class SSOEnablerCallback
  {
          public abstract void getSSOTokenSuccess(Bundle result);
          public abstract void getSSOTokenFailure(Bundle result);
  }
  ```

    * Success response bundle will contain:
        * SSO token as a string with key "SSOToken"
    * Failure response bundle will contain:
        * error code as an int with key "ErrorCode"
        * error description as a string with key "ErrorDescription"


* Get SSO token

  ```JAVA
  Bundle getSSOTokenAsync(Void);
  ```

* This API will provide the response via callback set during the init.

  **Ex**. call using singleton instance created during init:

  ```JAVA
  ssoEnabler.getSSOTokenAsync().
  ```


**Synchronous APIs**

* Get SSO Enabler instance and set the callback

  ```JAVA
  ssoEnabler = SSOEnabler.getInstance(context);</span>
  ```

* Get SSO token

  ```JAVA
  Bundle getSSOTokenSync(Void);
  ```

    * This API will block the caller thread and respond with the result bundle. Since this is a synchronous call, be sure to not use it im your main thread.

  ```JAVA
  void setSSOTokenTimeout(long);
  ```

    * Value in milliseconds. if set, override the default timeout value of 1 minute for sync API.


### Adobe Pass Clientless API update to use Dynamic Client Registration {#clientlessdcr}

If this is your first implementation please see the **Clientless Technical Overview** and contact Adobe in case you need support.

Adobe Clientless API requires applications to use Dynamic Client Registration in order to make calls to Adobe servers.

*   To use Dynamic Client Registration in your application, follow the instructions in [Dynamic Client Registration Management](./dcr-api/dynamic-client-registration-overview.md#dynamic-client-registration-management) to create a registered application and download a software statement.

*   To implement Dynamic Client Registration API to perform authentication and authorization requests to Adobe Pass servers, follow instructions in [Dynamic Client Registration Flow](./dcr-api/flows/dynamic-client-registration-flow.md).

### Adobe Pass Clientless API update to use Amazon SSO {#clientlesssso}

Amazon SSO payload obtained from Amazon SDK need to be present on requests made to Adobe Pass Authentication endpoints :

```
      /adobe-services/*
      /reggie/*
      /api/*
```


All Adobe Pass Authentication endpoints support the following methods to receive the Device-scoped identifier or Platform- Scoped identifier (present in Amazon SSO payload) :

* As a header : "Adobe-Subject-Token"
* As a query parameter : "ast"
* As a post parameter : "ast"


>[!NOTE]
>
>If the Device-scoped identifier or Platform-scoped identifier is sent as query/post parameter, then it must be included when generating the request signature.

>[!NOTE]
>
>Using query parameter "ast", the entire url may become very long and rejected. On /authenticate call, this parameter can be skipped as it was provided at /regcode call

**Examples:**

**Sending as custom header**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**Sending as query parameter**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**Sending as post parameter**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>If the Amazon SSO is not present or invalid, the Adobe Pass Authentication will ignore the attribute and the calls will be executed as if SSO is not present.
