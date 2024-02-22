---
Title: Channels
Description: Learn about channels and its configurations within TVE dashboard.
---

# Channels {#channels}

Channels are the themed sources of identifiable streams of video content provided by Multichannel Video Programming Distributors (MVPDs). These channels are characterized by their unique addresses and provide subscribers with continuous access to a specific range of content through Set-Top Box (STB).

When you select the **Channels** tab under **Configurations** in the left panel, a list of available channels for a particular programmer is displayed. This list presents key data about each channel in a tabular format. The data includes:

* **Display Name**: The brand name of a channel used for commercial purposes.

* **Channel Id**: A unique address of a channel within the system, also referred to as "requestor Id". It serves as a reference for internal processes and identification.

* **Integrations**: The number of connections established with MVPDs.

You can perform various operations with channels:

* [Manage channels](#manage-channels)
* [Add new channel](#add-new-channel)

## Manage channels {#manage-channels}

Select one of the available channels in the list to perform the following configurations:

* [General Settings](#general-settings)
* [Integrations](#integrations)
* [Certificates](#certificates)
* [Domains](#domains)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes)
    
### General settings {#general-settings}

You can edit the following details under **Channel information**:

* Change the brand name of a channel in **Display Name**.

* **Default Redirect URL** 

* **Error reporting**


**Analytics Configuration** - Configure Adobe Pass Authentication events to be forwarded to Adobe Analytics. Please contact Adobe for more details on how the Report Suite ID (RSID) needs to be configured before enabling this feature.

### Integrations {#integrations}

Contains the list of integrations with available MVPDs, alongside the status of each integration which might be enabled or not. Navigating to Integration page is available by clicking on a specific entry. 

### Certificates {#certificates}

Contains the list of certificates used in the authentication flow alongside their issuing organization, issuing date and expiry date. These certificates serve as Private/Public Keys and are used for validation purposes. 

### Domains {#domains}

Contains the list of domains from which the respective Channel will communicate with Adobe Pass Authentication. 

#### Add / Delete domains {#add-delete-domains}

To initiate the process of adding up a new domain for the selected channel, you need to click the "Add New Domain" button below the Domains list. This will create a new domain entry where you can specify the domain name. If a more generic domain already exists in the domains list, you shouldn't add a new subdomain.

![Add a new domain to a selected channel section](assets/add-domain-to-channel-sec.png)

*Figure: Domains tab in channels* 

### Registered Applications {#registered-applications}
    
Contains the list of application registrations. For more details, review the document [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

Contains the list of custom schemes. For more details, see [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

## Add new channel {#add-new-channel}