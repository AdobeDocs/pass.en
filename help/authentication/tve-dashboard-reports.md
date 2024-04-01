---
title: Reports
description: Learn how the data is aggregated in TVE dashboard reports.
---
# Reports {#Reports}

The Reports section of the TVE Dashboard provides access to aggregated data for different reports of your Channels integrations with various MVPDs across all [platforms](#platforms).

You can filter data and gather insights across [specific Channels or MVPDs](#selecting-specific-channels-mvpds) and [export](#export-reports) reports in comma separated values (CSV) file format for further analysis.

The **Reports** tab in the left panel presents [AuthN TTL Reports](#authn-ttl-reports) by default. To access other reports, select the following tabs at the top of the **Reports** section:

* [AuthZ TTL Reports](#authz-ttl-reports)
* [SSO Reports](#sso-reports)

## AuthN TTL reports {#authn-ttl-reports}

The AuthN TTL reports, also referred as authentication token time-to-live (TTL), displays the duration of the authentication token configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to visually inspect the amount of time a user remains authenticated for a specific MVPD and platform, with values presented in user-friendly formats like **days**, **hours**, **minutes**, and **seconds**. The AuthN TTL Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthN TTL value rather than the Adobe Pass Authentication configuration.

You can also view data for [specific Channels or MVPDs](#selecting-specific-channels-mvpds).

Use **Export** to download the data in CSV file. Learn more about how to [export report](#export-reports).

## AuthZ TTL reports {#authz-ttl-reports}

The AuthZ TTL reports, also referred to as authorization token time-to-live (TTL), displays the duration of the authorization token configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to visually inspect the amount of time a user remains authorized to watch content for a specific MVPD and platform, with values presented in user-friendly formats like **days**, **hours**, **minutes**, and **seconds**. The AuthZ TTL Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthZ TTL value rather than the Adobe Pass Authentication configuration.

You can also view data for [specific Channels or MVPDs](#selecting-specific-channels-mvpds).

Use **Export** to download the data in CSV file. Learn more about how to [export report](#export-reports).

## SSO Reports {#sso-reports}

The SSO reports, also referred as single sign-on status (SSO), displays the single sign-on status configured for your Channels integrations with various MVPDs across all [platforms](#platforms). These reports allow you to visually inspect the expected user authentication SSO experience for a specific MVPD and platform, with values presented as a tri-state like **SSO Disabled**, **SSO Enabled**, and **SSO Uncertain**. The SSO Reports table is designed with scrollable horizontal and vertical pages to accommodate various screen sizes.

>[!IMPORTANT]
>
> The **SSO Uncertain** placeholder is used where Single Sign-On (SSO) is enabled and possible. But the following settings might prevent SSO authentication:
>
> * User platform settings: For example, the option to block 3rd party cookies.
> * User decisions: For example, the users deny platform access to their TV Provider subscription.
> * MVPD settings: For example, MVPD requests authentication for each Channel.

You can also view data for [specific Channels or MVPDs](#selecting-specific-channels-mvpds).

Use **Export** to download the data in CSV file. Learn more about how to [export report](#export-reports).

## Platforms {#platforms}

The [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) presents data across various platforms in a tabular format. These platforms include:

* **DESKTOP**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication JavaScript SDK.

* **MOBILE: IOS**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication iOS SDK.

* **MOBILE: ANDROID**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication Android SDK.

* **MOBILE: OTHERS**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication REST API developed for mobile devices.

* **TVCD: ROKU**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication REST API and that are sending **Roku** as the device type.

* **TVCD: FIRETV**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication FireTV SDK.

* **TVCD: APPLETV**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication tvOS SDK.

* **TVCD: OTHERS**: Displays values that will be applied to the Programmer implementations over Adobe Pass Authentication REST API developed for TV connected devices.

* **PLATFORM: UNIDENTIFIED** Displays values that will be applied to the Programmer implementations for which Adobe Pass Authentication services detect an unknown device type.

To learn more about how to share the desired device type, such as **Roku** with Adobe Pass Authentication REST APIs or SDKs, view the mechanism of [passing client information](/help/authentication/passing-client-information-device-connection-and-application.md).

>[!IMPORTANT]
>
> The data aggregated is based on the specific configuration of each Adobe Pass Authentication environment. When switching between different TVE Dashboard environments, expect variations in the data across reports. Refer to the [Adobe Pass Authentication environments](/help/authentication/tve-dashboard-environments.md) to know more. 

## Selecting specific Channels and MVPDs {#selecting-specific-channels-mvpds} 

The [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) present data for **All Channels** integrations with **All MVPDs** by default.

To generate data for one or multiple channels:

1. Select **Included Channels** dropdown menu at the top of the desired report.
1. Deselect the specific options listed in **Included Channels** dropdown menu that you don't want to include in the reports.

To generate data for one or multiple MVPDs:

1. Select **Included MVPDs** dropdown menu at the top of the desired report.
1. Deselect the specific options listed in **Included MVPDs** dropdown menu that you don't want to include in the reports.

>[!NOTE]
>
>If you deselect **All Channels** or **All MVPDs** option in the respective dropdown menus, a message is displayed to select meaningful information to generate the report.

## Export reports {#export-reports}

To export data, navigate to the **Reports** tab in the left panel and select **Export report** at the upper-right corner of the desired report.
 
Depending on the respective report you've exported, a CSV file named **Adobe Pass - Reports - AuthN TTL.csv**, **Adobe Pass - Reports - AuthZ TTL.csv**, or **Adobe Pass - Reports - SSO.csv** will be automatically downloaded to your computer.

>[!NOTE] 
>
> Make sure that your browser's settings allow file downloads.

