---
title: Set up the license server database
description: Set up the license server database
copied-description: yes
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
---
# Set up the license server database{#set-up-the-license-server-database}

The reference implementation license server requires a database to support the following:

* User authentication 
* Usage model demo business rules 
* Metadata conversion 
* Domain support

Anonymous license acquisition does not require that the database be running.

>[!NOTE]
>
>This procedure applies only to Microsoft Windows. For other operating systems, see the documentation for your operating system or see the MySQL documentation.

To run the license server, you need to install and configure MySQL: 

1. On the DVD, go to the [!DNL Third Party\MySQL\Installer\5.1] folder and start the installation program.
1. Compete the MySQL installation.
1. Select **[!UICONTROL Configure MySQL Server Now]** to start the configuration wizard.
1. Until the fifth screen, use the default settings or select specific settings for your testing.
1. On the fifth screen, select **[!UICONTROL Online Transaction Processing (OLTP)]** or **[!UICONTROL Manual Setting]** and enter the maximum number of allowed connections.
1. Write down the root password.
1. To re-install MySQL, if you need to start the server later, complete the following steps:
   1. Delete the *system drive:* folder.
   
      This folder is located in [!DNL \Documents and Settings\All Users\Application Data\MySQL].   
   1. Delete the old MySQL install folder.
   
      For example, *system drive:*, which is located in [!DNL \Program Files\MySQL\MySQL Server 5.1].   
1. To install MySQL JDBC Driver 5.1.7, copy the [!DNL mysql-connector-java-5.1.7-bin.jar] file in the [!DNL Third Party\MySQL\Installer\5.1] folder on the DVD to the [!DNL ...\Tomcat6.0\lib] directory on the Tomcat Server.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 works with Tomcat 6.0. Older versions of Tomcat are no longer supported.
