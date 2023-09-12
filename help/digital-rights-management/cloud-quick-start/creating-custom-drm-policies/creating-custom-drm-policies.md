---
title: Create custom DRM policies (Optional)
description: Create custom DRM policies (Optional)
copied-description: yes
exl-id: a74f60b1-96a0-4fc4-bbf2-5db78f343562
---
# Create custom DRM policies (Optional){#create-custom-drm-policies-optional}

The Primetime Cloud DRM Protection Kit comes with a few pre-configured policies that can be used during packaging. If additional policy configurations are desired, for example, a specific SWF-allow listing right, the included Primetime DRM Policy Manager can be used to generate custom policies.

>[!NOTE]
>
>All policies must use ANONYMOUS authentication (not Username Password or Custom) - regardless of whether or not the Custom Auth/Entitlement workflow is used.

Included with the  Policy Manager is the [!DNL flashaccesstools.properties] configuration file, which has been modified to expose only the configurable policy options that  Primetime Cloud DRM  Service supports. Setting policy options that are not supported by the  Primetime Cloud DRM  Service will result in license acquisition errors. For information on using the Primetime DRM Policy Manager, refer to: [Primetime DRM Reference Implementations: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

To create a new policy, update the [!DNL flashaccesstools.properties] file as desired, and then use the command:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Create policies dynamically for Custom Auth/Entitlement{#create-policies-dynamically-for-custom-auth-entitlement}

If you are using  Primetime Cloud DRM Custom Authentication/Entitlement and want to dynamically create a new DRM policy for each license request (instead of pulling policies from a pre-generated pool), Adobe recommends that you use the Primetime DRM Java SDK directly. Using the Java SDK directly is faster than the [!DNL AdobePolicyManager.jar] tool, which automatically outputs the policy file to disk, incurring disk I/O overhead.

Sample code using the Java SDK can be found in the [!DNL /Primetime DRM PolicyManager/sampleCode/] directory, named [!DNL CreatePolicy.java] and [!DNL CreatePolicyWithOutputProtection.java]. Javadocs and documentation for the Java SDK can be found at [An Overview of Adobe Primetime DRM SDK](../../../digital-rights-management/drm-sdk-overview/overview.md)

To build and run the samples, please copy the .java files into the ../libs/ folder and run:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
