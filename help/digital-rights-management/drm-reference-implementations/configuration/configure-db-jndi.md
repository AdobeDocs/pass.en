---
title: Configure the license server database
description: Configure the license server database
copied-description: yes
exl-id: 1d5d988e-d22a-4405-8f39-1763f1f65094
---
# Configure the license server database{#configure-the-license-server-database}

To configure the sample database by setting up the database schema and populating the database with sample data: 

1. Bring up the MySQL command line.

   **On Windows -** Click  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **On Linux, etc.** - Type `MySQL`. 

1. Execute the following SQL script:

   mysql> source “ `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`”

   This script adds the user account `dbuser`, establishes a connection through a web application, and creates a database schema. 

   >[!NOTE]
   >
   >Ensure that there is no semicolon ( `;`) at the end of the script.

1. Edit the `PopulateSampleDB.sql` script that populates sample data in the tables to include data for your testing.

   This script is located in the `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` folder.
1. Execute the [!DNL PopulateSampleDB] script to populate the data as you did in step 2.

   >[!NOTE]
   >
   >The first time that you run the [!DNL CreateSampleDB.sql] script the following error occurs:

   You can safely ignore this error. It only occurs the first time you run this script. 

You need to configure the Database Connection Pooling (DBCP), which uses the Jakarta-Commons Database Connection Pool. A JNDI Datasource TestDB is configured to take advantage of this application server connection pooling. To change the database connection to point to a MySQL server that is not on localhost, modify one of the following files:

* The [!DNL META-INF\context.xml] file, which specifies the location, username, and password of the license server's database that is in the [!DNL flashaccess.war] file. 

* The `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` file.

and recreate the WAR file by using the updated files.

To change any of these parameters, edit the [!DNL context.xml] file in the [!DNL WebContent] directory and use the Ant script to recreate the WAR file. To tune the database, change the JNDI datasource settings in this file.

If you debug the Reference Implementation project in Eclipse, add `$CATALINA_HOME\lib\tomcat-dbcp.jar` to your run/debug configuration.

>[!NOTE]
>
>If you run the [!DNL flashaccess.war] file on a standalone Tomcat 6.0 server, this step is not required.
