---
title: Command line tools for packaging content and creating revocations lists 
description: Command line tools for packaging content and creating revocations lists 
copied-description: yes
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
---
# Command line tools for packaging content and creating revocations lists {#command-line-tools-for-packaging-content-revocation-lists}

The reference implementation includes the following command line tools:

* Policy Manager: A tool for creating and managing policies 
* Policy Update List Manager: A tool for creating and viewing policy update lists 
* Revocation List Manager: A tool for creating and viewing revocation lists 
* Media Packager: A tool for creating encrypted FLV and F4V files 
* AIR Publisher ID 
* UtilityLicense Generator 
* License Embedder

## Requirements {#requirements}

The requirements for using the command line tools available in the reference implementations are as follows:

* All of the command line tools require Java 1.5 or higher. 
* Packager and License Server credentials (certificate and password) that are issued by Adobe. You need credentials to encrypt and sign video files, to sign Policy Update and Revocation lists, and to pre-generate licenses.

>[!NOTE]
>
>Because of a Java bug, arguments that are used on the command line (such as file names, policy names, or descriptions) must use only characters from the operating system's default character set.

## Configuration file {#configuration-file}

Several of the command-line tools require a configuration file that contains information for the tools to use for applying policies and encrypting files.

The default configuration file is [!DNL flashaccesstools.properties]. It is located in the working directory; that is, the directory from which you run the tools (see Installing the command line tools). Each tool also contains an option ( `-c`) that lets you point to the configuration file you want to use if you prefer not to use the default.

The configuration file uses the Java property file format. If values for any of the properties contain special characters, keep in mind the following restrictions:

* Escape backslashes with an additional backslash. For example, to specify the [!DNL C:\credentials.pfx] file, specify it as [!DNL C:\\credentials.pfx] or `C:/credentials.pfx`. To specify a file on a network server, specify `\\\\server\\folder\\filename.pfx`. 
* The configuration file can contain only Latin-1 characters. If you must use non-Latin-1 characters, use the appropriate Unicode escape sequence (using, optionally, the [!DNL native2ascii] tool that comes with Java).

Set values for properties in the configuration file before you run the tools. For some of the command line tools, you can set the values for some options through either the command line or the configuration file. In those cases, values that are set through the command line take precedence over any values in the configuration file.

## Installing the command line tools  {#installing-the-command-line-tools}

You can copy the files you need from the [!DNL \Reference Implementation\Command Line Tools] directory on the DVD, which contains the default [!DNL flashaccesstools.properties] configuration file, and a [!DNL libs] directory, which contains the JAR files for the tools.

The [!DNL samples] directory contains several sample Java source files demonstrating usage of the Adobe Access SDK APIs. To build and run the samples, use the [!DNL build-samples.xml] Ant script.
