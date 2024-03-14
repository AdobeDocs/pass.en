---
title: Channels
description: Learn about channels and its configurations within TVE dashboard.
---

# Channels {#channels}

The Channels section of the TVE Dashboard allows you to access and manage settings for channels associated with a specific programmer. You can also [add a new channel](#add-new-channel).

The **Channels** section under **Configurations** in the left panel displays a list of linked channels with key details that include:

* **Display name**: The brand name of the channel used for commercial purposes.
* **Channel Id**: A unique identifier, also referred to as *requestor Id*.
* **Integrations**: The number of connections established with MVPDs.

To quickly locate a specific channel, enter the display name in **Search** at the top of the list.

## Manage channel configurations {#manage-channel-conf}

Navigate to the **Channels** section under **Configurations** in the left panel and select a desired channel from the list. You can then select the following tabs at the top to view and edit various settings:

* [General Settings](#general-settings)
* [Integrations](#integrations)
* [Certificates](#certificates)
* [Domains](#domains)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes) 

>[!IMPORTANT]
>
> To activate the configuration changes for each setting, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md). 

### General settings {#general-settings}

This tab presents Channel Information and Analytics Configuration.

#### Channel information {#channel-information}

* **Display name**: The brand name of the channel used for commercial purposes.

* **Default redirect URL**: The backup redirect URL for authentication and logout.

* **Error reporting**: If selected as **Yes**, the Adobe Pass SDKs will send error reports to the Adobe Pass backend for analytics purposes.

#### Analytics configuration {#analytics-configuration}

This section allows you to configure forwarding of Adobe Pass Authentication events to Adobe Analytics.

To enable **Analytics Configuration**, kindly contact your Technical Account Manager (TAM) for more details on how to configure the Report Suite ID (RSID).

### Integrations {#integrations}

This tab displays a list of available integrations of the currently selected channel with MVPDs, including the status of each integration, whether enabled or not. Select a specific entry from this list to access integration properties directly in the **Integrations** tab on the left panel. To know more, view [Integrations](/help/authentication/tve-dashboard-integrations.md).

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) and [inherited available certificates](#inherited-avail-certificates) used in the authentication and user metadata flows, providing key details about each certificate. The details include:

* The status (whether enabled for *user metadata encryption* usage or not) 
* Serial number
* Name of the issuer organization 
* Name of the subject organization
* Activation date
* Expiry date 
* A dropdown menu to encrypt user metadata (If you select **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

#### Available certificates {#available-certificates}

These certificates serve as private or public keys and play a crucial role in validation purposes.

You can make the following changes to available certificates:

* [Add new certificate](#add-new-certificate)
* [Delete certificate](#delete-certificate)

##### Add new certificate {#add-new-certificate}

To add new certificate, follow these steps:

1. Select **Add new certificate** at the top of the **Channels** section.
1. Paste the public key of your certificate in the **New certificate** dialog box.
1. Select **Add certificate**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Available Certificates** section will display the added certificate only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

To activate a new certificate, navigate to the list of **Available certificates** and select **Yes** from **Used to encrypted user metadata** dropdown menu.

##### Delete certificate {#delete-certificate}

To delete certificate, follow these steps: 

1. Hover over the desired certificate you want to delete from the list of **Available certificates**.
1. Select **Remove**.
1. Select **Delete** from the **Delete certificate** dialog box.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The certificate will be deleted from the **Available certificates** section only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

The deleted certificate will no longer be available for use.

#### Inherited available certificates {#inherited-avail-certificates}

Media companies define these certificates at their own level. All channels associated with the same media company can use these certificates.

### Domains {#domains}

This tab displays a list of available domains through which the respective channel communicates with Adobe Pass Authentication. You can make the following changes to domains:

* [Add new domain](#add-domains)
* [Delete domain](#delete-domain)

>[!TIP]
>
> Avoid adding a new subdomain if a more general domain exists in the list.

#### Add new domain {#add-domains}

To add domain, follow these steps:

1. Select **Add new domain** at the top of the **Available domains** section.
1. Add the name of your domain in **New domain** dialog box. 
1. Select **Add domain** to initiate adding a new domain for the selected channel.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Domain** tab will display the added domain only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

#### Delete domain {#delete-domain}

To delete domain, follow these steps:

1. Hover over the desired domain you want to delete from the list of **Available Domains**.
1. Select **Remove**.
1. Select **Delete** from the **Delete domain** dialog box.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The domain will be deleted from the **Available Domains** section only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

The deleted domain will no longer be available for use, and the application associated with this domain will lose access to the Adobe Pass authentication services.

### Registered Applications {#registered-applications}

This tab provides a list of application registrations. For more details, view [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. For more details, view [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

## Add new channel {#add-new-channel}

To add new channel, follow these steps:

1. Go to the **Channels** section under **Configurations** in the left panel.
1. Select **Add new channel** at the top of the list.
1. Select **Programmer Id** from the dropdown menu in the **New channel** dialog box.
1. Enter a unique identifier in **Channel Id**.
1. Enter the brand name of the channel used for commercial purposes in **Display name**. 
1. Select **Add channel**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Channels** section will display the added channel only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).
