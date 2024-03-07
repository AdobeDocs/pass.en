---
title: Channels
description: Learn about channels and its configurations within TVE dashboard.
---

# Channels {#channels}

When you log in to the TVE Dashboard, you can customize the settings for channels associated with a specific programmer. 

To configure channels in the TVE Dashboard, navigate to the **Channels** tab under **Configurations** in the left panel. 

A list of linked channels with key details is displayed. The details include:

* **Display Name**: The brand name of the channel used for commercial purposes.
* **Channel Id**: A unique identifier, also referred to as *requestor Id*.
* **Integrations**: The number of connections established with MVPDs.

To quickly locate a channel, you can enter the display name in **Search**.

You can perform the following actions with channels:

* [Manage channel configurations](#manage-channel-conf)
* [Add new channel](#add-new-channel)

## Manage channel configurations {#manage-channel-conf}

Navigate to the **Channels** tab under **Configurations** in the left panel and select the desired channel from the list to view and edit different settings in the following tabs:

* [General Settings](#general-settings)
* [Integrations](#integrations)
* [Certificates](#certificates)
* [Domains](#domains)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes) 

>[!IMPORTANT]
>
> To activate the configuration changes for all these tabs, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md). 

### General settings {#general-settings}

You can edit the following sections within this tab:

#### Channel information {#channel-information}

* **Display Name**: The brand name of the channel used for commercial purposes.

* **Default Redirect URL**: The backup redirect URL for authentication and logout.

* **Error reporting**: If selected as **Yes**, the Adobe Pass SDKs will send error reports to Adobe Pass backend for analytics purposes.

#### Analytics Configuration {#analytics-configuration}

This section allows you to configure Adobe Pass Authentication events to be forwarded to Adobe Analytics.

To enable **Analytics Configuration**, kindly contact Technical Account Manager (TAM) for more details on how to configure the Report Suite ID (RSID).

### Integrations {#integrations}

This tab displays a list of available integrations of current selected channel with MVPDs, including the status of each integration, whether it's enabled or not. Select a specific entry from this list to directly access integration properties page located under the **Integrations** tab in the left panel. To know more, view [Integrations](/help/authentication/tve-dashboard-integrations.md).

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) and [inherited available certificates](#inherited-avail-certificates) used in the authentication and user metadata flows, providing key details about each certificate. The details include the status (whether enabled for usage or not), serial number, the name of issuer organization and subject organization, activation date, expiry date, and a dropdown menu to encrypt user metadata (If selected as **Yes**, the certificate will be used to encrypt sensitive user information, such as zip code values).

#### Available Certificates {#available-certificates}

These certificates serve as private or public keys and play a crucial role in validation purposes.

#### Inherited Available Certificates {#inherited-avail-certificates}

These certificates are defined at the media company level. All channels associated with the same media company can use these certificates.

You can make the following changes to available certificates:

* [Add new certificate](#add-new-certificate)
* [Delete certificate](#delete-certificate)

#### Add new certificate {#add-new-certificate}

1. Select **Add new certificate** at the top of the channels page.
1. Paste the public key of your certificate in the **New certificate** dialog box.
1. Select **Add certificate**.

To activate a new certificate, select **Yes** from ***Used to encrypted user metadata** dropdown menu in the list of available certificates.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The new certificate will be added and activated only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

#### Delete certificate {#delete-certificate}

1. Hover over the desired certificate you want to delete from the list of **Available certificates**.
1. Select **Remove**.
1. Select **Delete** from the **Delete certificate** dialog box.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The certificate will be deleted only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

The deleted certificate will no longer be available for use.

### Domains {#domains}

This tab displays a list of available domains through which the respective channel communicates with Adobe Pass Authentication. You can make the following changes to domains:

* [Add new domain](#add-domains)
* [Delete domain](#delete-domain)

>[!TIP]
>
> If more general domain already exists in the list, avoid adding a new subdomain.

#### Add new domain {#add-domains}

1. Select **Add new domain** at the top of the **Available domains** section.
1. Add a name of your domain in **New domain** dialog box. 
1. Select **Add domain** to initiate the process of adding a new domain for the selected channel.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The new domain will be added only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

#### Delete domain {#delete-domain}

1. Hover over the desired domain you want to delete from the list of **Available Domains**.
1. Select **Remove**.
1. Select **Delete** from the **Delete domain** dialog box.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The domain will be deleted only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

The deleted domain will no longer be available for use, and the application associated with this domain will lose access to the Adobe Pass authentication services.

### Registered Applications {#registered-applications}

This tab provides a list of application registrations. For more details, view [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. For more details, view [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

## Add new channel {#add-new-channel}

To add new channel, follow these steps:

1. Go to the **Channels** tab under **Configurations** in the left panel.
1. Select **Add new channel** at the top of the list.
1. In the **New channel** dialog box, select **Programmer Id** from the dropdown menu.
1. Enter a unique identifier in **Channel Id**.

   >[!NOTE]
   >
   >It's essential to coordinate and confirm the **Channel Id** value in advance with your Technical Account Manager (TAM).

1. Enter the brand name of the channel used for commercial purposes in **Display name**. 
1. Select **Add channel**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The new channel will be added to the list on the **Channels** page only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).
