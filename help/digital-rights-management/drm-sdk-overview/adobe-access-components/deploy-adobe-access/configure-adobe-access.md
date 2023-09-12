---
title: Deploy Adobe Primetime DRM
description: Deploy Adobe Primetime DRM
copied-description: yes
exl-id: 64a96d70-502c-48b8-9f43-59f4001a7ab6
---
# Deploy Adobe Primetime DRM {#configure-adobe-primetime-drm}

A key advantage to Adobe Primetime DRM SDK is that you can install it on any Java™ application server or servlet container, such as Tomcat. You also need JDK™ 1.5 or higher. For more information on software requirements, see Primetime DRM SDK platform requirements: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

The high-level steps to deploy Primetime DRM are:

1. Install and configure Primetime DRM SDK. 
1. Obtain digital certificates from Adobe. 
1. Create a License Server using the SDK, or deploy Primetime DRM Server for Protected Streaming. 
1. Create content packaging and policy management tools to package content, use the provided content preparation tools, or license one of the Adobe HTTP Dynamic Streaming packagers. 
1. Define usage rules for your content, and create policies in support of those rules. 
1. Package your content using the packaging and policy management tools. 
1. Develop video applications with which consumers can view your protected content using Flash Player or Adobe AIR, or use an established OVP (Online Video Platform) that supports Primetime DRM. 
1. Deploy a SWF file for use with Flash Player to your website, or post the Adobe AIR installer for download.

These steps are expanded upon in the following sections, with references to other documents containing additional information.

## Deploying on a 64-bit operating system{#deploying-on-a-bit-operating-system}

A 64-bit operating system, such as the 64-bit version of RedHat or Windows, provides much better performance than a 32-bit operating system.

## Install Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK is provided as a Java archive (JAR) file. To learn more about installing Primetime DRM, see Using Adobe Primetime DRM SDK for Protecting Content and Secure Deployment Guidelines.

## Implement a License Server {#implement-a-license-server}

Using Adobe Primetime DRM SDK, you must create a License Server. When content is protected using Primetime DRM, it cannot be viewed until a license is issued to the consumer by the License Server. If identity-based licensing is used, password-based authentication ensures that only authorized consumers can open and view content.

When implementing a License Server, you must obtain the necessary digital certificates from Adobe. Refer to the Primetime DRM Certificate Enrollment document for detailed instructions on requesting certificates.

To learn more about implementing a License Server, and obtaining digital certificates, see **Using Adobe Primetime DRM SDK for Protecting Content.**

## Create content packaging and policy management tools{#create-content-packaging-and-policy-management-tools}

Using the Adobe Primetime DRM SDK, you can create content packaging and policy management tools. The policy management APIs allow administrators to create, view details of, and update policies. The packaging APIs embed the policy into video file, and encrypt the file using the content encryption key.

The Primetime DRM SDK includes a reference implementation ( [!DNL AdobePackager.jar]) that provides examples of content packaging and policy management tools ( [!DNL AdobePolicyManager.jar]).

To learn more about creating content packaging and policy management tools, see **Using the Adobe Primetime DRM SDK For Protecting Content.**

## Create policies and package content {#create-policies-and-package-content}

Using the usage rules supported by the SDK, you must define and create policies in support of your organization's business model, and then package your content using those policies. Once policies are applied to content during packaging, you can maintain control of your content no matter how widely it is distributed.

The policies in Adobe Primetime DRM support a wide range of different usage rules, including:

* Specifying the number of days a license is valid once a consumer begins watching the content. 
* Allowing license caching. 
* Specifying client runtimes and versions that can access content (for example, users must have a certain Adobe AIR application or a specific version of Flash Player). 
* Requiring that consumers authenticate themselves using a username and password prior to viewing protected content, or allowing anonymous access.

To learn more about packaging content, see *Protecting Content*. To learn more about the usage rules and the business models they support, see *Usage Rules*. 

## Develop applications for video playback {#develop-applications-for-video-playback}

To enable consumers to access and view content, develop a video playback application using Flash Player or Adobe AIR. Once you developed a video playback application, you must deploy it to consumers. If you are developing an application using Flash Player, host it on your organization's website. If you are developing an application using Adobe® AIR®, post the AIR application installer so that consumers can download and install the application on their computer.

To learn more about developing custom video playback applications for use with Adobe Primetime DRM, see the “Working with Video” chapter in [ActionScript 3.0 Developer Guide](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), the [Adobe Video Technology Center](https://www.adobe.com/devnet/video/), and the Open Source Media Framework.
