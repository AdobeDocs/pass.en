---
title: Building the Flash Access Manager AIR Application
description: Building the Flash Access Manager AIR Application
copied-description: yes
exl-id: f15fe9d2-d5e8-43ef-a1d5-1211752d54da
---
# Building the Flash Access Manager AIR Application {#building-the-flash-access-manager-air-application}

To build the Flash Access Manager AIR file from the source code, you need the Flex and AIR SDK installed on your machine. Before you can package and run the application, you must compile the MXML code into a SWF file using the [!DNL amxmlc] compiler. The [!DNL amxmlc] compiler can be found in the [!DNL bin] directory of the Flex 4 or later SDK. If desired, you can set your path environment variable to include the Flex SDK bin directory to make it easier to run the utilities on the command line.

Use the following procedure to build the Flash Access Manager AIR file:

1. Open a command shell or a terminal and navigate to the project folder of the Flash Access Manager AIR application ( [!DNL UI Tools\Flash Access Manager] in the Reference Implementation directory). 
1. Enter the following command: 

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Running [!DNL amxmlc] produces [!DNL FlashAccessManager.swf], which contains the compiled code of the application.

The Adobe AIR SDK includes the AIR Developer Tool (ADT) utility to package AIR applications and generate certificates. AIR applications should be digitally signed; users will receive a warning when installing applications that are not properly signed or are not signed at all. To generate a certificate using the command line, open a console window in the same folder as your AIR application and type the following:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Substitute *some_password* with a password of your choice. After a few seconds, ADT should complete its certificate generation process and you should have a new [!DNL testCert.pfx] file in your application directory.

Next, use ADT to package the application into an [!DNL .air] file, by using the command:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

This command tells ADT to package your application, using the key file in [!DNL testCert.pfx]. In the line above, you configure ADT to package your entire application into a file named [!DNL FlashAccessManager.air], and to include the files [!DNL FlashAccessManager-app.xml] and [!DNL FlashAccessManager.swf] and the images from the assets directory.

As part of this process, you'll be prompted for the password that you set for your new certificate file. Enter it, wait a moment, and a [!DNL FlashAccessManager.air] file should appear in the same directory as your project files.
