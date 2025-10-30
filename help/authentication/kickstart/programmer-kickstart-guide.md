---
title: Programmer kickstart guide
description: Programmer kickstart guide
exl-id: 0aecdb81-9b97-4475-b0b0-654d916b2374
---
# Programmer kickstart guide {#programmer-kickstart-guide}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This kickstart guide is intended for content providers (Programmers) who plan to integrate Adobe&reg; Pass Authentication into their websites or applications.

This document outlines key initial steps to ensure a smooth and efficient start to the integration process. It aims to clarify expectations and provide guidance on how we will collaborate with partners to achieve successful integrations.

Adobe provides a range of resources to help you integrate Adobe Pass Authentication into your website or application. Please refer to the **"You will provide"** and **"Adobe will provide"** mentions from each section below.

## Setup process {#setup-process}

The setup process involves among others the following steps:

![Adobe&reg; Pass Authentication Integration Process](/help/authentication/assets/progr-flow-int-lifecycle.png)

*Adobe&reg; Pass Authentication Integration Process*

**You will provide** during the kickoff phase:

* **Service provider (requestor identifier)**

  This is a string that will uniquely identify the brand of the website or the application that is making requests to Adobe Pass Authentication. The string itself is arbitrary but needs to be agreed between Adobe and the Programmer

* **Channel information**

  This is a set of strings used to identify the content channel(s) requested by the service provider. In many cases, the channel and service provider are the same. However, a single identifier can represent multiple content channels. These channel name strings should align with the corresponding cable TV channels. Note that some MVPDs may validate this value during the authentication and/or authorization process.

* **Domain names**

  This list will include the actual domain names listed to Adobe to represent the service provider. It ensures that only your authorized domains can access Adobe Pass Authentication using your metadata. Be sure to provide and clearly identify domain names for both production and staging (testing) environments, as these may differ.

**You will provide** via MVPD:

* **Credential sets**

  These are credentials used to authenticate and authorize, or solely authenticate, the user with the MVPD. Typically, these credentials consist of a username and password, which the MVPD will supply to you for both profiles (staging and production).

* **Resource identifiers**

  These are unique identifiers for the content channels, shows, episodes, or assets that the service provider wants to protect. These identifiers are used to request authorization decisions and must be agreed upon with the MVPD.

>[!IMPORTANT]
>
> The Programmer is responsible for coordinating with the MVPD to finalize any necessary business agreements. Meanwhile, Adobe Pass Authentication will collaborate with the MVPD to ensure the technical integration is properly established:
>
> * **New MVPD**
>
>     If the MVPD is not integrated with Adobe, custom code must be developed based on the MVPD specific requirements. Until this development is completed, the MVPD will not be available, and product testing with that MVPD cannot proceed.
>
> * **Existing MVPD**
>
>     If the MVPD is already integrated with Adobe, the connectivity process is significantly streamlined. In most cases, connectivity can be established quickly through configuration adjustments rather than extensive development.
>
> All integrations require joint quality assurance (QA) efforts, including testing by the MVPD, as the end user is ultimately a customer of the MVPD. Coordinating test cycles often depends on the MVPD's resource availability, which can introduce potential delays.

## Access to customer support {#access-customer-support}

**Adobe will provide** access to our customer support system via [Zendesk](https://tve.zendesk.com/home). To access Zendesk, you must register and create an account at https://tve.zendesk.com/home. There is no limit to the number of users you can register. Once registered, you can view and share comments on any submitted ticket.

The Adobe Pass Authentication team is available to assist you with any questions or technical issues you may encounter during the integration process. Please contact us at [tve-support@adobe.com](mailto:tve-support@adobe.com).

## Access to documentation {#access-documentation}

**Adobe will provide** access to our public documentation via [Adobe Experience League](https://experienceleague.adobe.com/en/docs/pass/authentication/home).

The Adobe Pass Authentication team provides comprehensive documentation for the available features and APIs under the [Integration Guide for Programmers](/help/authentication/integration-guide-programmers/programmer-integration-guide-overview.md) section. Refer to the table of contents under this section for links to detailed information on each topic.

## Access to testing tool {#access-testing-tool}

**Adobe will provide** access to our APIs exploration tool via [Adobe Developer](https://developer.adobe.com/adobe-pass/) website.

## Access to configuration management tool {#access-configuration-management-tool}

**Adobe will provide** access to a self-service tool for managing your configuration and data via [Adobe Pass TVE Dashboard](https://experience.adobe.com/pass/authentication).

The Adobe Pass Authentication team provides comprehensive documentation for the usage of the TVE Dashboard under the [User Guide for TVE Dashboard](/help/authentication/user-guide-tve-dashboard/tve-dashboard-overview.md) section. Refer to the table of contents under this section for links to detailed information on each topic.
