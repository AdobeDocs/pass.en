---
title: Reports
description: Learn how the data is aggregated in TVE dashboard reports.
---
# Reports {#Reports}

Reports allow you to [view](#view-reports) and [export](#export-reports) aggregated data across [specific Channels and their integrations with various MVPDs](#selecting-specific-channels-mvpds) across all [platforms](#platforms).

## Platforms {#platforms}

When you go to the **Reports** tab under **Stats** in the left panel, the [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) tabs on the top present data across various platforms in a tabular format. These platforms include:

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
>[AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) aggregate data based on the specific configuration of each Adobe Pass Authentication environment. When switching between different TVE Dashboard environments, expect variations in the data across reports. Refer to the [Adobe Pass Authentication environments](/help/authentication/tve-dashboard-environments.md) to know more. 

## Selecting specific Channels and MVPDs {#selecting-specific-channels-mvpds} 

You can apply filters to aggregate data across specific Channels or MVPDs for the [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports). When you go to the **Reports** tab under **Stats** in the left panel, these reports present data for **All Channels** integrations with **All MVPDs** by default.

To generate data for one or multiple channels:

1. Select **Included Channels** dropdown menu at the top of the desired report.
1. Deselect the specific options listed in **Included Channels** dropdown menu that you don't want to include in the reports.

To generate data for one or multiple MVPDs:

1. Select **Included MVPDs** dropdown menu at the top of the desired report.
1. Deselect the specific options listed in **Included MVPDs** dropdown menu that you don't want to include in the reports.

>[!NOTE]
>
>If you deselect **All Channels** or **All MVPDs** option in the respective dropdown menus, a message is displayed to select meaningful information to generate the report.

## View reports {#view-reports}

When you log in to the TVE Dashboard, navigate to the **Reports** tab under **Stats** in the left panel. You can access and [export](#export-reports) the following reports:

* [AuthN TTL Reports](#authn-ttl-reports)
* [AuthZ TTL Reports](#authz-ttl-reports)
* [SSO Reports](#sso-reports)

### AuthN TTL reports (#authn-ttl-reports)

This report displays the Time-To-Live (TTL) of the authentication token configured for your Channels integrations with various MVPDs across all [platforms](#platforms).

The authentication token Time-To-Live also referred as AuthN TTL, is displayed in human readable values such as days, hours, minutes, and seconds.

The AuthN TTL reports allow you to visually inspect the amount of time a user will remain authenticated, considering a specific MVPD and platform.

To access AuthN TTL reports, select the **AuthN TTL Reports** tab from the **Reports** section.

The AuthN TTL Reports table contains pages that can be scrolled horizontally and vertically based on your screen size.

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthN TTL value rather than the Adobe Pass Authentication configuration.

### AuthZ TTL reports {#authz-ttl-reports}

This report displays the Time-To-Live (TTL) of the authorization token configured for your Channels integrations with various MVPDs across all [platforms](#platforms).

The authorization token Time-To-Live also referred to as AuthZ TTL, is displayed in human readable values such as days, hours, minutes, and seconds.

The AuthZ TTL reports allow you to visually inspect the amount of time a user will be authorized to watch content, considering a specific MVPD and platform.

To access AuthZ TTL reports, select the **AuthZ TTL Reports** tab from the **Reports** section.

The AuthZ TTL Reports table contains pages that can be scrolled horizontally and vertically based on your screen size.

>[!IMPORTANT]
>
> The **Set by MVPD** placeholder is used when the MVPD enforces the AuthZ TTL value rather than the Adobe Pass Authentication configuration.

### SSO Reports {#sso-reports}

This report displays the Single Sign-On (SSO) status configured for your Channels integrations with various MVPDs across all [platforms](#platforms).

The Single Sign-On status also referred as SSO status, is displayed as a tri-state with possible values such as SSO Disabled, SSO Enabled, and SSO Uncertain.

The SSO reports allow you to visually inspect the expected user authentication SSO experience, considering a specific MVPD and a specific platform.

The SSO Reports table contains pages that can be scrolled horizontally and vertically based on your screen size.

>[!IMPORTANT]
>
> The **SSO Uncertain** placeholder is used where Single Sign-On (SSO) is enabled and possible. But the following settings might prevent SSO authentication:
>
> * User platform settings: For example, the option to block 3rd party cookies.
> * User decisions: For example, the users deny platform access to their TV Provider subscription.
> * MVPD settings: For example, MVPD requests authentication for each Channel.

## Export reports {#export-reports}

The [AuthN TTL Reports](#authn-ttl-reports), [AuthZ TTL Reports](#authz-ttl-reports), and [SSO Reports](#sso-reports) allow to export data in a Comma separated Values (CSV) file format.

To export data, select **Export report** at the upper-right corner of the desired report.
 
Depending on the respective report you've exported, a file named **Adobe Pass - Reports - AuthN TTL.csv**, **Adobe Pass - Reports - AuthZ TTL.csv** or **Adobe Pass - Reports - SSO.csv** will be downloaded automatically to your computer.

>[!NOTE] 
>
> Make sure that your browser's settings allow file downloads.

