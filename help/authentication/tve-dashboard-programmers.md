---
title: Programmers
description: Learn about programmers and its configurations within TVE dashboard.
---
# Programmers {#programmers}

>[!NOTE]
>
>The content on this page is provided for information purposes only. The usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The **Programmers** section of the TVE Dashboard allows you to view and manage settings for the [programmers](/help/authentication/glossary.md#programmer) linked to your account entitlements. You can also [add a new programmer](#add-new-programmer) as per your requirement.

The **Programmers** tab in the left panel displays a list of existing programmers with the following details:

* **Programmer ID**: A media company identifier within the system.
* **Channels**: The number of associated channels linked to a programmer.

![List of existing programmers](assets/programmers-list.png)

*List of existing programmers*

Type the name of the programmer in the **Search** bar above the list to know more about a programmer.

## Manage programmer configurations {#manage-programmer-conf}

Follow these steps to manage various settings of a specific programmer.

1. Select the **Programmers** tab in the left panel.
1. Select a programmer from the list. 
1. Select one of the following tabs to view and edit corresponding settings of the selected programmer:

   * [Channels](#channels)
   * [Certificates](#certificates)
   * [Registered Applications](#registered-applications)
   * [Custom Schemes](#custom-schemes)

   ![Programmer settings](assets/programmer-settings.png)

   *Programmer settings*

>[!IMPORTANT]
>
> View [Review and push changes](/help/authentication/tve-dashboard-review-push-changes.md) for more information on activating the configuration changes.

### Channels {#channels}

This tab displays a list of channels linked with a current programmer. Select a specific channel from this list to access detailed information in the [Channels](/help/authentication/tve-dashboard-channels.md) section.

To add a new channel for the selected programmer, select **Add new channel** from the upper-right corner of **Available Channels** section. Learn [how to add a new channel](/help/authentication/tve-dashboard-channels.md#add-new-channel).

   ![Add a new channel](assets/programmers-channels.png)

   *Add a new channel*

### Certificates {#certificates}

This tab displays a list of [available certificates](#available-certificates) used in the user metadata encryption flows. It displays details about each certificate that includes:

* The status (whether enabled for **user metadata encryption** usage or not) 
* Serial number
* Name of the issuer organization 
* Name of the subject organization
* Issued date
* Expiry date 
* A dropdown menu to encrypt user metadata (If you select **Yes**, the certificate will encrypt sensitive user information, such as zip code values).

#### Available certificates {#available-certificates}

These certificates serve as private or public keys and are used for user metadata encryption. All channels associated with the same media company can use these certificates.

You can make the following changes to available certificates:

* [Add new certificate](#add-new-certificate)
* [Delete certificate](#delete-certificate)

##### Add new certificate {#add-new-certificate}

Follow these steps to add a new certificate.

1. Select **Add new certificate** at the upper-right corner of the **Available Certificates** section.

   ![Add a new certificate](assets/programmer-add-new-certificate.png)

   *Add a new certificate*

1. Paste the public key of your certificate in the **New certificate** dialog box.
1. Select **Add certificate**.

   A new configuration change has been created and is ready for server update. To use the new certificate listed in the **Available Certificates** section, proceed with the [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md) flow.

1. Locate the new certificate in the list of **Available Certificates**.

   >[!IMPORTANT]
   >
   > Make sure that your systems are up to date and ready to use the new certificate.

1. Select **Yes** from **Used to encrypted user metadata** dropdown menu to activate a new certificate.

##### Delete certificate {#delete-certificate}

Follow these steps to delete a certificate.

1. Hover on the certificate you want to delete from the list of **Available certificates**.
1. Select **Remove**.

   ![Remove the selected certificate](assets/programmer-remove-certificate.png)

   *Remove the selected certificate*

1. Select **Delete** on the **Delete certificate** dialog box.

A new configuration change has been created and is ready for server update. The certificate will be deleted from the **Available certificates** section only after [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md).

### Registered Applications {#registered-applications}

This tab provides a list of application registrations. View [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md), for more information.

### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. View [iOS/tvOS application registration](/help/authentication/iostvos-application-registration.md) and [Dynamic client registration management](/help/authentication/dynamic-client-registration-management.md), for more information.

## Add new programmer {#add-new-programmer}

Follow these steps to add a new programmer entity.

1. Select the **Programmers** tab in the left panel.
1. Select **Add new programmer** at the upper-right corner of the **Programmers** section.

   ![Add a new programmer](assets/add-new-programmer.png)

   *Add a new programmer*

1. Type media company identifier in **Programmer ID** in the **New programmer** dialog box.
1. Type a commercial brand name you want to be shown in the console under **Display name**. 
1. Select **Add programmer**.

A new configuration change has been created and is ready for server update. To use the new programmer listed in the **Programmers** section, proceed with the [review and push changes](/help/authentication/tve-dashboard-review-push-changes.md) flow.

