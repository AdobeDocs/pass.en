---
title: Initial Flash Access Manager setup
description: Initial Flash Access Manager setup
copied-description: yes
exl-id: 880822f3-0d21-42fc-889e-7375a2aab11a
---
# Initial Flash Access Manager setup {#initial-flash-access-manager-setup}

Use the following procedure to set up Flash Access Manager:

1. Deploy the Packager Server. This server should only be available to users within your firewall (do not deploy this software on a public-facing machine). For more information on deploying the server, see [Deploying the license server and watched folder packager](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

    * Copy [!DNL flashaccess-packager.war] to Tomcat's webapps folder.
    * Copy [!DNL flashaccess-refimpl-packager.properties] from resources to a location on the classpath.
    * Start the server. You will see some errors due to problems in the properties file; this is expected since the properties have not been filled in yet.

1. Install the Flash Access Manager AIR application by launching the [!DNL .air] file (requires AIR 1.5 or higher).
1. Launch the Flash Access Manager AIR application.

   If your server is running somewhere other than `https://localhost:8080*`, you see errors stating that the application cannot connect to the server. Dismiss the error dialog and fill in the correct URL for the Packager Server URL in the Preferences Tab. If the server is running at the specified URL and the properties file is on the classpath, the Preferences screen will be populated with the values in the properties file. After you set the packager server URL, the AIR application remembers this setting, and you will not have to enter it the next time you launch the application.
1. Fill in the values in the Preferences tab and click **[!UICONTROL Save]**. 
1. If you want to use the Watched Folders, you will need to restart the server to recover from the errors you saw in Step 3. If the preferences are configured properly, no errors should appear during startup.
