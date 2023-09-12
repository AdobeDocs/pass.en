---
title: About command-line tools configuration files
description: About command-line tools configuration files
copied-description: yes
exl-id: 0ec4917e-7c70-4b84-86ac-c34c8a522018
---
# About command-line tools configuration files{#about-command-line-tools-configuration-files}

The command-line tools look for [!DNL flashaccesstools.properties] in the directory in which you run the tools. However, you can use the `-c` option when you run a command-line tool to specify a different location for the default [!DNL flashaccesstools.properties]. You can also use `-c` to specify a different configuration file.

The command-line tools configuration files use the *Java property file* format, for which the following rules apply:

* Escape backslashes with an additional backslash.

  For example, on a Windows machine, to specify the [!DNL C:\credentials.pfx] file, you need to enter it as [!DNL C:\\credentials.pfx] or `C:/credentials.pfx`. To specify a file on a Windows network server, you need to enter `\\\\server\\folder\\filename.pfx` 
* Include only *Latin-1* characters.

  To use non-*Latin-1* characters, you need to use the appropriate Unicode escape sequence. You can optionally apply the [!DNL native2ascii] tool (included with Java) to your configuration file entries.
