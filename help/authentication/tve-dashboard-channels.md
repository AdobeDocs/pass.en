---
title: Channels
description: Learn about channels and their various configurations within TVE dashboard.
---

# Channels {#channels}

The Channels section of the TVE Dashboard allows you to view and manage settings for the existing channels associated with a specific programmer. You can also [add a new channel](#add-new-channel) as per your requirement.

The **Channels** tab in the left panel displays a list of linked channels with key details that include:

* **Display name**: The brand name of the channel used for commercial purposes.
* **Channel ID**: A unique identifier, also referred to as requestor ID.
* **Integrations**: The number of connections established with MVPDs.

![List of existing Channels](assets/channels-list.png)

*List of existing Channels*

To quickly locate a specific channel, enter the **Display name** in **Search** at the top of the list.

## Manage channel configurations {#manage-channel-conf}

To manage various settings of a specific Channel:

1. Navigate to the **Channels** tab in the left panel.
1. Select the required Channel from the available list. 
1. At the top of the **Channels** section, you'll see several tabs for different settings: 

   * [General Settings](#general-settings)
   * [Integrations](#integrations)
   * [Certificates](#certificates)
   * [Domains](#domains)
   * [Registered Applications](#registered-applications)
   * [Custom Schemes](#custom-schemes) 

   Select the respective tab to view and edit the settings associated with the selected channel.

   ![Select the required settings](assets/channel-settings.png)

   *Select the required settings*

>[!IMPORTANT]
>
> To activate the configuration changes for each setting, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md). 

### General settings {#general-settings}

This tab presents Channel Information and Analytics Configuration.

#### Channel information {#channel-information}

In this section, you can edit the following details:

* **Display name**: The brand name of the channel used for commercial purposes.

* **Default redirect URL**: The backup redirect URL for authentication and logout.

* **Error reporting**: If selected as **Yes**, the Adobe Pass SDKs will send error reports to the Adobe Pass backend for analytics purposes.

![Edit Channel information](assets/channel-information.png)

*Edit Channel information*

#### Analytics configuration {#analytics-configuration}

This section allows you to configure forwarding of Adobe Pass Authentication events to Adobe Analytics.

To enable **Analytics Configuration**, kindly contact your Technical Account Manager (TAM) for more details on how to configure the Report Suite ID (RSID).

![Enable Analytics Configurations](assets/channel-analytical-conf.png)

*Enable Analytics Configurations*

You can select **Add new analytics configuration** to add multiple configurations.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The new configuration will be added only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

### Integrations {#integrations}

This tab displays a list of available integrations between the currently selected channel and MVPDs. It lists each integration along with its status, indicating whether it's enabled or not. Select a specific entry from this list to access detailed information in the [Integrations](tve-dashboard-integrations.md) section.

![List of Available Integrations](assets/channel-integrations.png)

*List of Available Integrations*

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) and [inherited available certificates](#inherited-avail-certificates) used in the authentication and user metadata flows. It displays key details about each certificate that includes:

* The status (whether enabled for *user metadata encryption* usage or not) 
* Serial number
* Name of the issuer organization 
* Name of the subject organization
* Activation date
* Expiry date 
* A dropdown menu to encrypt user metadata (If you select **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

#### Available certificates {#available-certificates}

These certificates serve as Private/Public Keys and are used for validation purposes.
You can make the following changes under available certificates section:

* [Add new certificate](#add-new-certificate)
* [Delete certificate](#delete-certificate)

##### Add new certificate {#add-new-certificate}

To add new certificate, follow these steps:

1. Select **Add new certificate** at the top of the **Available Certificates** section.

   ![Select Add new certificate](assets/add-new-certificate.png)

   *Select Add new certificate*

1. Paste the public key of your certificate in the **New certificate** dialog box.
1. Select **Add certificate**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Available Certificates** section will display the added certificate only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

To activate a new certificate, navigate to the list of **Available certificates** and select **Yes** from **Used to encrypted user metadata** dropdown menu.

##### Delete certificate {#delete-certificate}

To delete certificate, follow these steps: 

1. Hover over the required certificate you want to delete from the list of **Available certificates**.
1. Select **Remove**.

   ![Select Remove](assets/channel-delete-certificate.png)

   *Select Remove*

1. Select **Delete** from the **Delete active certificate** dialog box.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The certificate will be deleted from the **Available certificates** section only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

The deleted certificate will no longer be available for use.

#### Inherited available certificates {#inherited-avail-certificates}

Media companies define these certificates at their own level. All channels associated with the same media company can use these certificates.

   ![Inherited available certificates](assets/inherited-available-certificates.png)

   *Inherited available certificates*

### Domains {#domains}

This tab displays a list of available domains through which the respective channel communicates with Adobe Pass Authentication. 

You can make the following changes to domains:

* [Add new domain](#add-domains)
* [Delete domain](#delete-domain)

>[!TIP]
>
> Avoid adding a new subdomain if a more general domain exists in the list.

#### Add new domain {#add-domains}

To add domain, follow these steps:

1. Select **Add new domain** at the top of the **Available domains** section.

   ![Select Add new domain](assets/add-new-domain.png)

   *Select Add new domain*

1. Add the name of your domain in **New domain** dialog box. 

1. Select **Add domain** to initiate adding a new domain for the selected channel.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Domain** tab will display the added domain only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

#### Delete domain {#delete-domain}

To delete domain, follow these steps:

1. Hover over the desired domain you want to delete from the list of **Available Domains**.
1. Select **Remove**.

   ![Select Remove](assets/remove-domain.png)

   *Select Remove*

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

1. Go to the **Channels** tab in the left panel.
1. Select **Add new channel** at the top of the **Channels** section.

   ![Select Add new channel](assets/add-new-channel.png)

   *Select Add new channel*

1. Select **Programmer ID** from the dropdown menu in the **New channel** dialog box.

1. Enter a unique identifier in **Channel ID**.
1. Enter the brand name of the channel used for commercial purposes in **Display name**. 
1. Select **Add channel**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Channels** section will display the added channel only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

