---
title: Programmers
description: Learn about programmers and its configurations within TVE dashboard.
---
# Programmers {#programmers}

The Programmers section of the TVE Dashboard allows you to access and manage settings for [programmers](/help/authentication/glossary.md#programmer) associated your account entitlements. You can also [add new programmer](#add-new-programmer).

The **Programmers** section under **Configurations** in the left panel displays the following details of a programmer:

* **Programmer Id**: A media company identifier within the system.
* **Channels**: The number of associated channels linked to a programmer.

To quickly locate a specific programmer, enter the display name in **Search** at the top of the list.

## Manage programmer configurations {#manage-programmer-conf}

Navigate to the **Programmers** section under **Configurations** in the left panel and select a desired programmer. You can then select the following tabs at the top to view and edit various settings: 

* [Channels](#channels)
* [Certificates](#certificates)
* [Registered Applications](#registered-applications)
* [Custom Schemes](#custom-schemes) 

>[!IMPORTANT]
>
> To activate the configuration changes for each setting, view [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md). 

### Channels {#channels}

This tab displays a list of channels linked with a current programmer. Select a specific **Channel** from this list to access channel properties directly in **Channels** section on the left panel. For more details, refer to the intructions for [Channels](/help/authentication/tve-dashboard-channels.md).

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) used in the authentication flow, providing key details about each certificate. The details include:

* The status (enabled for usage or not) 
* Serial number
* Name of the issuer organization 
* Name of the subject organization
* Activation date
* Expiry date 
* A dropdown menu to encrypt user metadata (If you select **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

#### Available certificates {#available-certificates}

These certificates serve as private or public keys and play a crucial role in validation purposes. All channels associated with the same media company can use these certificates.

You can make the following changes to available certificates:

* [Add new certificate](#add-new-certificate)
* [Delete certificate](#delete-certificate)

##### Add new certificate {#add-new-certificate}

To add new certificate, follow these steps:

1. Select **Add new certificate** at the top of the **Programmers** section.
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

### Registered Applications {#registered-applications}

This tab provides a list of application registrations. For more details, view [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md).

### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. For more details, view [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md)

## Add new programmer {#add-new-programmer}

To add new programmer entity, follow these steps:

1. Go to the **Programmers** section under **Configurations** in the left panel.
1. Select **Add new programmer** at the top of the list.
1. Enter a media company identifier in **Programmer Id** in the **New programmer** dialog box.
1. Enter a commercial brand name you want to be shown in the console under **Display name**. 
1. Select **Add programmer**.

>[!NOTE]
>
>A new local configuration change is pending and ready to be pushed to the server. The **Programmers** section will display the added programmer only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

