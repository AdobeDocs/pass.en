---
title: Programmers
description: Learn about programmers and its configurations within TVE dashboard.
exl-id: b450d7cc-d5b5-4454-8f95-8047856bfb98
---
# Programmers {#programmers}

>[!NOTE]
>
>The content on this page is provided for information purposes only. The usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The **Programmers** section of the TVE Dashboard allows you to view and manage settings for the [programmers](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#programmer) linked to your account entitlements. You can also [add a new programmer](#add-new-programmer) as per your requirement.

The **Programmers** tab in the left panel displays a list of existing programmers with the following details:

* **Programmer ID**: A media company identifier within the system.
* **Channels**: The number of associated channels linked to a programmer.

![List of existing programmers](../assets/tve-dashboard/new-tve-dashboard/programmers/programmers-list-view.png)

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

   ![Programmer settings](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-tabs-view.png)

   *Programmer settings*

>[!IMPORTANT]
>
> View [Review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md) for more information on activating the configuration changes.

### Channels {#channels}

This tab displays a list of channels linked with a current programmer. Select a specific channel from this list to access detailed information in the [Channels](/help/authentication/user-guide-tve-dashboard/tve-dashboard-channels.md) section.

To add a new channel for the selected programmer, select **Add new channel** from the upper-right corner of **Available Channels** section. Learn [how to add a new channel](/help/authentication/user-guide-tve-dashboard/tve-dashboard-channels.md#add-new-channel).

   ![Add a new channel](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-add-new-channel-button.png)

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

   ![Add a new certificate](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-add-new-certificate-button.png)

   *Add a new certificate*

1. Paste the public key of your certificate in the **New certificate** dialog box.

1. Select **Add certificate**.

1. Locate the new certificate in the list of **Available Certificates**.

   >[!IMPORTANT]
   >
   > Make sure that your systems are up to date and ready to use the new certificate.

1. Select **Yes** from **Used to encrypted user metadata** dropdown menu to activate a new certificate.

A new configuration change has been created and is ready for server update. To use the new certificate listed in the **Available Certificates** section, proceed with the [review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md) flow.

##### Delete certificate {#delete-certificate}

Follow these steps to delete a certificate.

1. Hover on the certificate you want to delete from the list of **Available certificates**.

1. Select **Remove**.

   ![Remove the selected certificate](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-remove-certificate-button.png)

   *Remove the selected certificate*

1. Select **Delete** on the **Delete certificate** dialog box.

A new configuration change has been created and is ready for server update. The certificate will be deleted from the **Available certificates** section only after [review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md).

### Registered Applications {#registered-applications}

This tab displays a list of registered applications. For more details related to registered applications usage, refer to the [dynamic client registration overview](../integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

You can make the following actions with registered applications:

* [Add a new registered application](#add-registered-applications)
* [Download a software statement](#download-software-statement)

#### Add new registered application {#add-registered-applications}

Follow these steps to add a new registered application.

1. Select **Add new application** at the upper-right corner of the **Registered Applications** section.

   ![Add a new application](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-add-new-application-button.png)

   *Add a new application*

1. Select **Assigned to Channel** from the dropdown menu in the **New Application** dialog box.

   >[!IMPORTANT]
   >
   > It is recommended to create registered applications with more specific and limited permissions to enhance security and prevent unauthorized access. Therefore, when creating registered applications, consider using narrower options for the assigned `channel`.

1. Select **Platforms** from the dropdown menu.

   >[!IMPORTANT]
   >
   > It is recommended to create registered applications with more specific and limited permissions to enhance security and prevent unauthorized access. Therefore, when creating registered applications, consider using narrower options for the assigned `platforms`.

1. Select **Domains** from the dropdown menu.

   >[!IMPORTANT]
   >
   > In the client registration process, the client application can request to be permitted to use a redirect URL for the finalization of the authentication flow. When a client application uses a specific redirect URL, it is validated against the `domains` picked in this selection.

1. Type the **Name** of the application.

1. Type the **Version** of the application.

   >[!IMPORTANT]
   >
   > It is recommended to create a new registered application for each major update of your client application to manage its life cycle and usage. If necessary, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) to revoke a registered application in order to block the functionality of a specific client application version.

1. Select **Type** value "DIRECT" from the dropdown menu.

1. Select **Add application**.

A new configuration change has been created and is ready for server update. To use the new registered application listed in the **Registered Applications** section, proceed with the [review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md) flow.

#### Download software statement {#download-software-statement}

Follow these steps to download a software statement.

1. Hover on the registered application you want to download the software statement from the list of **Registered Applications**.

1. Select **Download**.

   ![Download a software statement](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-download-software-statement-button.png)

   *Download a software statement*


### Custom Schemes {#custom-schemes}

This tab displays a list of custom schemes. For more details related to custom schemes usage, refer to the [iOS/tvOS application registration](/help/authentication/integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-application-registration.md).

You can make the following changes to custom schemes:

* [Generate a new custom scheme](#generate-custom-schemes)

#### Generate new custom scheme {#generate-custom-schemes}

Follow these steps to generate a new custom scheme.

1. Select **Generate new custom scheme**.

   ![Generate a new custom scheme](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-add-new-custom-scheme-button.png)

   *Generate a new custom scheme*

A new configuration change has been created and is ready for server update. To use the new custom scheme listed in the **Custom Schemes** section, proceed with the [review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md) flow.

## Add new programmer {#add-new-programmer}

Follow these steps to add a new programmer entity.

1. Select the **Programmers** tab in the left panel.

1. Select **Add new programmer** at the upper-right corner of the **Programmers** section.

   ![Add a new programmer](../assets/tve-dashboard/new-tve-dashboard/programmers/programmer-add-new-programmer-button.png)

   *Add a new programmer*

1. Type media company identifier in **Programmer ID** in the **New programmer** dialog box.

1. Type a commercial brand name you want to be shown in the console under **Display name**.

1. Select **Add programmer**.

A new configuration change has been created and is ready for server update. To use the new programmer listed in the **Programmers** section, proceed with the [review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md) flow.
