---
title: Programmers
description: Learn about programmers and its configurations within TVE dashboard.
---
# Programmers {#programmers}

Programmers in the TVE Dashboard, also known as networks, are subsidiary companies of a larger corporation that owns and manages one or more channels within their domain.

When you log in to the TVE Dashboard, you can customize the settings for a [programmer](/help/authentication/glossary.md#programmer).

>[!NOTE]
>
> You can only adjust settings for one programmer at a time based on your current login credentials.

To configure programmers in TVE Dashboard, navigate to the **Programmers** tab under **Configurations** in the left panel.

The details for a programmer is displayed as follows:

* **Programmer ID**: A reference ID within the system that helps in identifying a specific programmer.
* **Channels**: The number of associated channels linked to the programmer.

Select programmer to perform the following actions:

* [Manage programmer configurations](#manage-programmer-conf)
* [Add new programmer](#add-new-programmer)

## Manage programmer configurations {#manage-programmer-conf}

Navigate to the **Programmers** tab under **Configurations** in the left panel and select a programmer to view and edit different settings in the following tabs:

* [Channels](#channels)
* [Certificates](#certificates)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes) 

>[!IMPORTANT]
>
> To activate the configuration changes for all tabs mentioned above, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md). 

### Channels {#channels}

This tab a list of channels linked with a logged in programmer. Select a specific **Channel** from the list to directly access the **Channels** tab in the left panel. To know more, refer to the intructions for [Channels](/help/authentication/tve-dashboard-channels.md).

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) used in the authentication flow, providing key details about each certificate. The details include the status (whether enabled for usage or not), serial number, the name of issuer organization and subject organization, activation date, expiry date, and a drop-down option to encrypt user metadata dropdown (If selected as **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

#### Available Certificates {#available-certificates}

These certificates serve as private or public keys and play a crucial role in validation purposes.#### Add new certificate {#add-new-certificate}

#### Add new certificate {#add-new-certificate}

1. Select **Add new certificate** at the top of the channels page.
1. Paste the public key of your certificate in the **New certificate** dialog box.
1. Select **Add certificate**.

A new configuration is created and ready to be pushed to the server. The certificate will be added only after review and push changes. For more details, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

#### Remove certificate {#remove-certificate}

1. Hover over the desired certificate you want to delete from the list of **Available certificates**.
1. Select **Remove**.
1. Select **Delete** from the **Delete certificate** dialog box.

The deleted certificated will no longer be available for use.

### Registered Applications {#registered-applications}

This tab provides a list of application registrations. For more details, view [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. For more details, view [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

## Add new programmer {#add-new-programmer}

To add new programmer entity, follow these steps:

1. Go to the **Programmers** tab under **Configurations** in the left panel.
1. Select **Add new programmer** at the top of the list.
1. In the **New programmer** dialog box, enter a media company identifier in **Programmer Id**.
1. Enter a commercial brand name you want to display in console in **Display name**. 
1. Select **Add programmer**.

A new configuration is created and ready to be pushed to the server. The new programmer will be added to the list on the **Programmers** page only after review and push changes. For more details, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

