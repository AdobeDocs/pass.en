---
title: Adobe Primetime authentication (Optional)
description: Adobe Primetime authentication (Optional)
copied-description: yes
exl-id: 59fbbefa-0c84-474a-ace9-141b50ad5f5f
---
# Adobe Primetime authentication (Optional) {#adobe-primetime-authentication-optional}

If the DRM policy that is used to package the content is an anonymous policy, a license will be issued to all license requests. Optionally,  Primetime Cloud DRM  also supports authentication via Adobe Primetime authentication. If this feature is enabled, a license will not be issued unless the client device has first acquired a Primetime authentication Token and set it locally via the appropriate client API ( `setAuthenticationToken`) for setting custom authentication tokens. For more information on integrating Primetime authentication into your authentication workflow, please refer to: [Adobe Primetime authentication.](https://tve.helpdocsonline.com/home)

During license acquisition, if the DRM Policy states that Pri metime authentication is required, the license server will parse and validate the Primetime authentication Short Media Token. If the DRM policy specifies a `ResourceID` or `RequestorID`, the license server will also validate the token against these properties. If they are not set, the license server will specify the property(ies) as "null" during token validation. Only if token validation is successful will a license be issued; otherwise, a 3328 DRMErrorEvent with a 305 sub-error-code (User Not Authorized) will be dispatched by the client.

Primetime authentication parameters must be specified in the policy used to package the content that is destined to require Primetime authentication.

The relevant properties are:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>When using Primetime authentication in conjunction with the (DRM) License Rotation feature, please bear in mind that the Primetime authentication Short Media Token (SMT) has a short validity date. If your application plans to make use of License Rotation (e.g., to support the *Blackouts* use case), the application must be aware of this and refresh its Primetime authentication Short Media Token prior to rotating its license.
