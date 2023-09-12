---
description: You can set up the Reference Implementation to use Adobe Analytics reporting.
title: Configure Adobe Analytics Reporting
exl-id: 3607f9d4-1069-4722-af0b-121223125112
---
# Configure Adobe Analytics Reporting {#configure-adobe-analytics-reporting}

You can set up the Reference Implementation to use Adobe Analytics reporting.

The Reference Implementation is configured to send Primetime authentication event data to Adobe Analytics using the Adobe Mobile Library bundled within the Primetime SDK. To enable and use the event data sent from the application, you must first create an Adobe Analytics account. Once the account is created:

1. Configure the application with your account information; and
1. Create processing rules to customize how the event data is displayed within your reports.

The table below presents the data sent to Adobe Analytics:

|  Action Name  | `a.media.pass.event.MvpdSelection`  | The user selected a Multi-channel Video Programming Distirbutor (MVPD) in a selection dialog  |
|---|---|---|
|  Context Data  | `a.media.pass.MvpdId (String)`  | The user-selected MVPD  |
|  | `a.media.pass.ClientType`  | (String) The client type as either "flash", "html5", "ios", or "android"  |
|  | | |
|  Action Name  | `a.media.pass.event.AuthenticationDetection`  | An Authentication workflow completed  |
|  Context Data  | `a.media.pass.Successful`  | (Boolean) Whether the token request was successful, true or false  |
|  | `a.media.pass.MvpdId`  | (String) The user-selected MVPD  |
|  | `a.media.pass.Guid`  | (String) A tracking ID  |
|  | `a.media.pass.Cached`  | (Boolean) Token already in cache, true or false  |
|  | `a.media.pass.ClientType`  | (String) The client type as either "flash", "html5", "ios", or "android"  |
|  | | |
|  Action Name  | `a.media.pass.event.AuthorizationDetection`  | An Authorization workflow completed  |
|  Context Data  | `a.media.pass.Successful`  | (Boolean) Whether the token request was successful, true or false  |
|  | `a.media.pass.MvpdId`  | (String) The user selected MVPD  |
|  | `a.media.pass.Guid`  | (String) A tracking ID  |
|  | `a.media.pass.Cached`  | (Boolean) Token already in cache, true or false  |
|  | `a.media.pass.Error`  | (String) The error if the authorization attempt failed  |
|  | `a.media.pass.ErrorDetails`  | (String) Further error details  |
|  | `a.media.pass.ClientType`  | (String) The client type as either "flash", "html5", "ios", or "android"  |

1. Configure the application for use with Adobe Marketing Cloud.

   To enable sending Primetime Primetime authentication data to Adobe Analytics, an [!DNL `ADBMobileConfig.json`] configuration file must be added to the Reference Implementation at compile time. Note that this is exactly the same configuration file used by the Primetime SDK to send Video Analytics data to the Marketing Cloud. Please consult the [Adobe Marketing Cloud documentation](https://microsite.omniture.com/t2/help/en_US/reference/) for more information on configuring an application with your Adobe Analytics account.
1. Create processing rules.

   The Primetime authentication event data sent by the Reference Implementation will not automatically appear in your analytics reports. You must first make use of the data by creating processing rules. Please consult the [Adobe Analytics documentation on creating processing rules](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
