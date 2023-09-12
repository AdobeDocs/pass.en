---
title: Policy workflow details
description: Policy workflow details
copied-description: yes
exl-id: e3daf7a9-def0-48a9-8190-adb25eec7b59
---
# BEES Workflow {#bees-workflow}

**Summary:**

* **Policy** - Create a DRM BEES-aware policy that indicates BEES is required for all content packaged using thispolicy.
* **Packaging** - Package content using the BEES-aware DRM policy.
* **Authentication** - Authenticate your client device and use the Primetime DRM API, or the Primetime API, toassociate this token with Primetime Cloud DRM. Doing this will cause the client device to send this authenticationtoken up to Primetime Cloud DRM along with all license requests. Primetime Cloud DRM will not process thistoken, but instead will pass it along (as an opaque blob) to your BEES endpoint for processing.
* **Licensing** - Request a license for your protected content. The client device will automatically append yourpreviously-set authentication token to the call.
* **Entitlement** - Primetime Cloud DRM will determine that the content was packaged with a policy that requiresBEES. Primetime Cloud DRM will construct a JSON request to send to the BEES endpoint. The BEES responsewill instruct Primetime Cloud DRM on whether or not to issue a license, and optionally, which DRM policy to use.

## Policy workflow details {#policy-workflow-details}

When Primetime Cloud DRM processes a license request, it parses the DRM policy in the request to determine if a call to a backend-entitlement service is required before the content can be shown. If a BEES call *is* required,  Primetime Cloud DRM will create the BEES request, then parse the DRM policy to obtain a specified BEES URL endpoint for the BEES request. 

Apply your DRM policy that indicates the BEES requirement, specifying the following two custom properties in the policy:

* `policy.customProp.1=bees.required=<true | false>` 
* `policy.customProp.2=bees.url=<url to your BEES endpoint>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

For example, using the  Primetime DRM Policy Manager ( [!DNL AdobePolicyManager.jar]), you would specify the following two custom properties in the [!DNL flashaccesstools.properties] configuration file:

* `policy.customProp.1=bees.required=true` 
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>If you are already using `policy.customProp.1` or `policy.customProp.2` for another property, simply use unique numbers for the newer properties.

## Package workflow details {#package-workflow-details}

During the packaging of your Adobe Access-protected content, you must apply one of your BEES-aware DRM policies to the content.

## Authentication workflow details {#authentication-workflow-details}

In order for your BEES endpoint to make entitlement decisions, the client device must provide authentication information. You accomplish this by using your own customer-specific authentication token.

Primetime Cloud DRM  does not have to understand this token - it simply passes this token through to your BEES endpoint. The client device is responsible for creating or acquiring this token and setting it using the `DRMManager.setAuthenticationToken()` API.

Do the following to associate this token with  Primetime Cloud DRM , so that it is sent with the license request:

   Instantiate the `DRMManager` object with the DRM metadata of the content that was packaged for  Primetime Cloud DRM.

   The `setAuthenticationToken()` method works by associating the given byte array with the License Server URL provided in the DRM metadata that was used to instantiate `DRMManager`.

   ```java
   //client device acquires auth token needed by your BEES endpoint  
   DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
   mgr.setAuthenticationToken(<auth token>);
   ```

The token gets sent with all license requests until the token is cleared by calling `.setAuthenticationToken` with null as the parameter.

## License workflow details{#license-workflow-details}

Request a license from Primetime Cloud DRM by calling `mgr.loadVoucher()`.

## Entitlement request and response details{#entitlement-request-and-response-details}

When  Primetime Cloud DRM determines that content was packaged with a BEES-aware DRM policy, it constructs the following JSON request to send to the BEES endpoint specified in the DRM policy:

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}

```

The following response is expected from the BEES endpoint:

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}

```

Primetime Cloud DRM uses the response to determine whether or not it should issue a license to the requesting device, and if it should substitute a new DRM policy into the license generation process. If `isAllowed` is `true` and no policy is provided in the response, then the original DRM Policy used during content packaging time will be used to generate the license.
