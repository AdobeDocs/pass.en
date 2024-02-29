---
title: Channels
description: Learn about channels and its configurations within TVE dashboard.
---

# Channels {#channels}

In TVE Dashboard, channels are the primary sources of video content provided by Multichannel Video Programming Distributors (MVPDs). These channels are characterized by their unique addresses and provide subscribers with continuous access to a specific range of content through Set-Top Box (STB). 

This page provides an overview of configuring channels within TVE Dashboard. To configure channels in TVE Dashboard:

1. Log in with your authorized programmer credentials.
1. Select **Channels** tab under **Configurations** in the left panel. A list of available channels for a particular programmer is displayed. This list presents key details about each channel. The details include:

* **Display Name**: The brand name of the channel used for commercial purposes.
* **Channel Id**: A unique address within the system, also known as **requestor Id** that serves as a reference for internal processes and identification.

* **Integrations**: The number of connections established with MVPDs.

You can perform various operations with channels:

* [Manage channel configurations](#manage-channel-conf)
* [Add new channel](#add-new-channel)

## Manage channel configurations {#manage-channel-conf}

You can select a channel from the list to view and edit different settings in the following tabs:

* [General Settings](#general-settings)
* [Integrations](#integrations)
* [Certificates](#certificates)
* [Domains](#domains)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes)
    
### General settings {#general-settings}

You can edit the following two sections within this tab:

**Channel information**

* **Display Name**: The Channel's commercial name.

* **Default Redirect URL**: The backup redirect URL for authentication and logout.

* **Error reporting**: If selected as **Yes**, the Adobe Pass SDKs will send error reports to Adobe Pass backend for analytics purposes.

**Analytics Configuration**

* Allows you to configure Adobe Pass Authentication events to be forwarded to Adobe Analytics. 
* If you want to enable this feature, please contact Adobe for more details on how to configure the Report Suite ID (RSID).

### Integrations {#integrations}

This tab displays a list of integrations with available MVPDs, indicating the status of each integration, whether it's enabled or not. By selecting a specific integration entry, you can directly navigate to  Integrations. Know more about Integrations.

### Certificates {#certificates}

This tab displays of list of available certificates and inherited available certificates used in the authentication flow, providing key details about each certificate. The details include the status (whether enabled for usage or not), serial number, the name of issuing organization and subject organization, issuing date, expiry date, and a drop-down option to encrypt user metadata dropdown (If selected as **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

**Available Certificates**

These certificates serve as private/public keys and and play a crucial role in validation purposes. 

**Inherited Available Certificates**

These certificates are defined at the media company level. All channels associated with the same media company can use these certificates.

**Add new certificate**

1. Select **Add new certificate** at the upper-right of the channels page.
1. Paste the new certificate in the **New certificate** dialog.
1. Select **Add certificate**. 

<!--A new configuration will be created and ready to be pushed to the server. The certificate will be added only after the configuration push.-->

### Domains {#domains}

Contains the list of domains from which the respective Channel will communicate with Adobe Pass Authentication. 

**Add / Delete domains** {#add-delete-domains}

To initiate the process of adding up a new domain for the selected channel, you need to click the "Add New Domain" button below the Domains list. This will create a new domain entry where you can specify the domain name. If a more generic domain already exists in the domains list, you shouldn't add a new subdomain.

![Add a new domain to a selected channel section](assets/add-domain-to-channel-sec.png)

*Figure: Domains tab in channels* 

### Registered Applications {#registered-applications}
    
Contains the list of application registrations. For more details, review the document [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

Contains the list of custom schemes. For more details, see [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

