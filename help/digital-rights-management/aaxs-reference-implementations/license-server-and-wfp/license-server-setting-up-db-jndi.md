---
title: Setting up the database and configuring the JNDI datasource
description: Setting up the database and configuring the JNDI datasource
copied-description: yes
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
---
# Setting up the database and configuring the JNDI datasource {#setting-up-the-database-and-configuring-the-jndi-datasource}

The reference implementation license server requires a database to support the following features:

* User authentication 
* Usage model demo business rules 
* Metadata conversion 
* Domain support

Anonymous license acquisition does not require a database to be running.

>[!NOTE]
>
>The instructions in this section are for the Microsoft Windows platform. For other operating systems, see the documentation for your operating system or see the MySQL documentation.

To run the license server, you will need to install and configure MySQL 5.1.34:

1. Run the MySQL installer (found in the Third Party\MySQL\Installer\5.1 folder on the DVD). 
1. At the end of the installation procedure, check **[!UICONTROL Configure MySQL Server Now]** to start the configuration wizard. Use the default settings or select specific settings for your testing purposes, with the exception that on the 5th screen you must select **[!UICONTROL Online Transaction Processing (OLTP)]** or **[!UICONTROL Manual Setting]** and enter the maximum number of connections allowed. 

1. Make a note of the root password. 
1. If you need to re-install MySQL, follow these steps to avoid problems in starting the server afterward:

    * Delete the folder *system drive:* [!DNL \Documents and Settings\All Users\Application Data\MySQL]. 
    
    * Delete the old MySQL install folder: for example, *system drive:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Next, you will need to install MySQL JDBC Driver 5.1.7. To do this, copy [!DNL mysql-connector-java-5.1.7-bin.jar] (found in the [!DNL Third Party\MySQL\Installer\5.1] folder on the DVD) to Tomcat Server lib directory: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC Driver 5.1.7 works with Tomcat 6.0. Older versions of Tomcat are not supported.

Set up the sample database by setting up the database schema and populating the database with sample data. To do this, perform the following steps:

1. Go to  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** . 
1. After typing in the password, execute the following SQL script to add the user account `dbuser` for establishing a connection through a web application and create database schema (make sure that there is no ";" at the end. Just press enter.): 

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Edit the script that populates sample data in the tables to include data for your testing purposes: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql]. 
1. Execute this script to populate the data as you did in Step 2.

>[!NOTE]
>
>The first time you run the [!DNL CreateSampleDB.sql] script you will receive the following error:

*ERROR 1396 (HY000): Operation DROP USER failed for 'dbuser'@'localhost' Query OK, 0 rows affected (0.00 sec).*

You can safely ignore this error. This only happens the first time you run this script.

At this point you will need to configure Database Connection Pooling (DBCP). DBCP uses the Jakarta-Commons Database Connection Pool. A JNDI Datasource TestDB is configured to take advantage of this application server connection pooling. To change database connection to point to a MySQL server that is not on localhost, modify the [!DNL META-INF\context.xml] file (which specifies the location, username, and password of the license server's database) located in [!DNL flashaccess.war], or modify [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] and recreate the WAR file using the updated files. To change any of these parameters, edit the [!DNL context.xml] located in the WebContent directory and use the Ant script to recreate the WAR file. To tune the database, change the JNDI datasource settings in this file.

If you debug the Reference Implementation project within Eclipse, you need to add `$CATALINA_HOME\lib\tomcat-dbcp.jar` to your run/debug configuration. This step is not required if you run the [!DNL flashaccess.war] file on a standalone Tomcat 6.0 server.
