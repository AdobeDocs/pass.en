---
title: MVPD kickstart guide
description: MVPD kickstart guide
exl-id: 6423cc9a-a45a-4cde-b562-4cb72c98e505
---
# MVPD kickstart guide {#mvpd-kickstart-guide}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This kickstart guide is intended for Multichannel Video Programming Distributors (MVPDs) who plan to integrate with Adobe&reg; Pass Authentication.

This document outlines key initial steps to ensure a smooth and efficient start to the integration process. It aims to clarify expectations and provide guidance on how we will collaborate with partners to achieve successful integrations.

Adobe provides a range of resources to help you to integrate with Adobe Pass Authentication. Please refer to the **"You will provide"** and **"Adobe will provide"** mentions from each section below.

>[!CAUTION]
>
> Each time a user initiates an entitlement flow, they are assigned a single, opaque, unique user ID. This ID, originating from the MVPD, is used to identify the user within a Programmer's app.
>
> <br/>
>
> The user ID must not contain any Personally Identifiable Information (PII) or data that could be used alone or in combination with other details to identify, contact, or locate the user.

## Setup process {#setup-process}

The setup process involves among others the following steps:

![Adobe&reg; Pass Authentication Integration Process](/help/authentication/assets/mvpd-int-lifecycle.png)

*Adobe&reg; Pass Authentication Integration Process*

### Kickoff {#kickoff}

**You will provide** during the kickoff phase:

* **Display name**

    This is a string displayed on Programmer websites or applications when prompting users to select their Pay TV provider.

* **Logo URL**

    This is a file, measuring 112 by 33 pixels, containing the logo displayed on Programmer websites or applications when prompting users to select their Pay TV provider.

* **Time-to-Live (TTL)**

    The TTL is a value typically set by the MVPD as part of the authentication or authorization processes. However, Adobe can override those TTL values and provide different values depending on what is agreed upon by both the Programmer and the MVPD.

* **Credential sets**

    These are credentials used to authenticate and authorize, or solely authenticate, the user with the MVPD. Typically, these credentials consist of a username and password, which must be supplied for both profiles (staging and production).

### Metadata exchange (SAML) {#metadata-exchange-saml}

**Adobe will provide** during the metadata exchange phase:

* **Staging environment metadata**

    Adobe's SP metadata can be retrieved from https://sp.auth-staging.adobe.com/sp/metadata.

* **Production environment metadata** 

    Adobe's SP metadata can be retrieved from https://sp.auth.adobe.com/sp/metadata.

**You will provide** during the metadata exchange phase:

* **Staging metadata**

    The MVPD's metadata for the staging environment.

* **Production metadata**

    The MVPD's metadata for the production environment.

### Connectivity {#connectivity}

**You will provide** a way to allowlist IPs from Adobe, as Adobe Pass Authentication requires firewalls to permit traffic through ports 80 and 443 to enable access to restricted resources during both authentication and authorization processes.

**You will provide** a deployment in the staging profile to test the connectivity.

### Development {#development}

**Adobe will provide** engineering time to work closely with the MVPD to ensure the technical integration is correctly established. This process involves developing custom code tailored to the MVPD's specific requirements.

### Deployment in staging {#deployment-staging}

**Adobe will provide** a build with the required code updates that will first be deployed in the PRE-QUAL staging environment. During this phase, the necessary configuration changes will also be implemented to integrate the MVPD with the `TestDistributors` service provider for testing purposes.

**You and Adobe will provide** quality assurance (QA) time to ensure that the integration is successfully tested in the PRE-QUAL staging environment. After this phase, the MVPD will be moved to the RELEASE staging environment for further testing with an actual Programmer.

### Deployment in production {#deployment-production}

**You will provide** a deployment in the production profile to test the connectivity.

**Adobe will provide** a build with the required code updates that will be deployed in the PRE-QUAL production environment. 

**You and Adobe will provide** quality assurance (QA) time to ensure that the integration is successfully tested using the production profile. If everything is okay at this point, Adobe can move the integration to the RELEASE production environment ("live"), which is available to all users.

>[!IMPORTANT]
>
> Once the integration is live in the RELEASE production environment, maintaining an optimal customer experience is paramount. To address server-down scenarios effectively, MVPDs must provide detailed escalation procedure documentation to Adobe for managing such issues.
>
> In return, Adobe ensures that MVPDs receive the latest version of the Adobe Pass Authentication escalation process for streamlined issue resolution.

## Access to environments {#access-environments}

**Adobe will provide** access to environments for different stages of the development process:

* **Prequalification (PRE-QUAL)**

    The PRE-QUAL environment hosts the next release candidate and serves as the initial integration platform for new partners. Before moving to the RELEASE environment, partners are given time to test their integration in PRE-QUAL.

* **Release (RELEASE)**

    The RELEASE environment hosts the current (stable) production build.

For more information on how to use these environments, refer to the [Understanding the Adobe Environments](/help/authentication/notes-technical/environments/understanding-the-adobe-environments.md) documentation.

>[!IMPORTANT]
> 
> Configuration changes to these environments must be explicitly requested through your Adobe representative, following the established change request process.
 
## Access to customer support {#access-customer-support}

**Adobe will provide** access to our customer support system via [Zendesk](https://tve.zendesk.com/home). To access Zendesk, you must register and create an account at https://tve.zendesk.com/home.

The Adobe Pass Authentication team is available to cover any questions or technical issues we may encounter during the integration process. Please contact us at [tve-support@adobe.com](mailto:tve-support@adobe.com).

## Access to documentation {#access-documentation}

**Adobe will provide** access to our public documentation via [Adobe Experience League](https://experienceleague.adobe.com/en/docs/pass/authentication/home).

The Adobe Pass Authentication team provides comprehensive documentation for the available features and workflows under the [Integration Guide for MVPDs](/help/authentication/integration-guide-mvpds/mvpd-integration-guide-overview.md) section. Refer to the table of contents under this section for links to detailed information on each topic.

## Access to testing tool {#access-testing-tool}

**Adobe will provide** access to our APIs exploration tool via [Adobe Developer](https://developer.adobe.com/adobe-pass/) website.
