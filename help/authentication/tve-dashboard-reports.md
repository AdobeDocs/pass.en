---
title: Reports
description: Learn how the data is aggregated in TVE Dashboard reports.
---
# Reports {#Reports}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The **Reports** section of the TVE Dashboard provides access to aggregated data for AuthN TTL, AuthZ TTL, and SSO reports. These reports include your channel integrations with different MVPDs across all [platforms](#platforms).

Reports let you to filter data and gather insights across [specific Channels or MVPDs](#selecting-specific-channels-mvpds). You can also export reports in a CSV file for further analysis.

## View reports {#view-reports}

Follow these steps to view a specific report.

1. Select the **Reports** tab in the left panel.
1. Select one of the following tabs to view and export aggregated data of the included channels and MVPDs:
   * [AuthN TTL Reports](#authn-ttl-reports)
   * [AuthZ TTL Reports](#authz-ttl-reports)
   * [SSO Reports](#sso-reports)

   ![Type of reports](assets/type-of-reports.png)

   *Type of reports*

### AuthN TTL reports {#authn-ttl-reports}

The AuthN TTL reports, also referred as Authentication Time-To-Live (TTL), displays the duration of the authentication token configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to inspect the amount of time a user remains authenticated for a specific MVPD and platform. The values are presented in user-friendly formats such as, **days**, **hours**, **minutes**, and **seconds**. The AuthN TTL Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

You can also view and download data for [specific channels or MVPDs](#selecting-specific-channels-mvpds).

![Export AuthN TTL Reports](assets/authn-ttl-reports.png)

*Export AuthN TTL Reports*

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthN TTL value rather than the Adobe Pass Authentication configuration.

Select **Export reports** to save the data as a CSV file on your local machine.

### AuthZ TTL reports {#authz-ttl-reports}

The AuthZ TTL reports, also referred to as Authorization Time-To-Live (TTL), displays the duration of the authorization token configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to inspect the amount of time a user remains authorized to watch content for a specific MVPD and platform. The values are presented in user-friendly formats such as, **days**, **hours**, **minutes**, and **seconds**. The AuthZ TTL Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

You can also view and download the data for [specific channels or MVPDs](#selecting-specific-channels-mvpds).

![Export AuthZ TTL Reports](assets/authz-ttl-reports.png)

*Export AuthZ TTL Reports*

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthZ TTL value rather than the Adobe Pass Authentication configuration.

Select **Export reports** to save the data as a CSV file on your local machine. 

### SSO Reports {#sso-reports}

The SSO reports, also referred as single sign-on, displays the single sign-on status configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to inspect the expected user authentication SSO experience for a specific MVPD and platform. The values are presented in user-friendly formats such as, **SSO Disabled**, **SSO Enabled**, and **SSO Uncertain**. The SSO Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

You can also view and download data for [specific channels or MVPDs](#selecting-specific-channels-mvpds).

![Export SSO Reports](assets/sso-reports.png)

*Export SSO Reports*

>[!IMPORTANT]
>
> The **SSO Uncertain** placeholder is used where Single Sign-On (SSO) is enabled and possible. But the following settings might prevent SSO authentication that is explained in the examples below:
>
> * User platform settings: The option to block third-party cookies.
> * User decisions: The users deny platform access to their TV provider subscription.
> * MVPD settings: MVPD requests authentication for each channel.

Select **Export reports** to save the data as a CSV file on your local machine.

## Platforms {#platforms}

The [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) present data across various platforms, such as:

* **Desktop**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication JavaScript SDK.

* **Mobile** 

   **iOS**: Displays values that will be applied to the programmer implementations over the Adobe Pass Authentication iOS SDK.

   **Android**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication Android SDK.

   **Others**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication REST API developed for mobile devices.

* **TVCD**

   **Roku**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication REST API and that are sending Roku as a device type.

   **FireTV**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication FireTV SDK.

   **AppleTV**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication tvOS SDK.

   **Others**: Displays values that are applied to the programmer implementations over the Adobe Pass Authentication REST API developed for TV connected devices.

* **Platform unidentified**: Displays values that are applied to the Programmer implementations for which Adobe Pass Authentication services detect an unknown device type.

To learn more about how to share the desired device type, such as **Roku** with Adobe Pass Authentication REST APIs or SDKs, view the mechanism of [passing client information](/help/authentication/passing-client-information-device-connection-and-application.md).

>[!IMPORTANT]
>
> The data aggregated is based on the specific configuration of each Adobe Pass Authentication environment. When switching between different TVE Dashboard environments, expect variations in the data across reports. Refer to the [Adobe Pass Authentication environments](/help/authentication/tve-dashboard-environments.md) to know more. 

## Selecting specific channels and MVPDs {#selecting-specific-channels-mvpds} 

The [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) present data for **All Channels** integrations with **All MVPDs** by default.

>[!NOTE]
>
> If you deselect **All Channels** or **All MVPDs** in the respective dropdown menus, a message is displayed to make a selection to view meaningful reports.

To generate a report for specific channels:

1. Select the **Included Channels** dropdown menu at the top of the selected report.

   ![Included Channels dropdown menu](assets/include-channels.png)

   *Included Channels dropdown menu*

1. Deselect **All Channels**.
1. Select the required channels from the **Included Channels** dropdown menu for which you want to generate data.


>[!NOTE]
>
> To have options available in the **Included MVPDs** dropdown menu, you must select at least one channel in the **Included channels** dropdown menu.

To generate a report for specific MVPDs:

1. Select the **Included MVPDs** dropdown menu at the top of the selected report.

   ![Included MVPDs dropdown menu](assets/include-mvpds.png)

   *Included MVPDs dropdown menu*

1. Deselect **All MVPDs**.
1. Select the required MVPDs from the **Included MVPD's** dropdown menu for which you want to generate data.





