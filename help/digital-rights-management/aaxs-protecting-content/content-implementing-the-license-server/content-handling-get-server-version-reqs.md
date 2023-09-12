---
title: Handling Get Server Version requests
description: Handling Get Server Version requests
copied-description: yes
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
---
# Handling Get Server Version requests{#handling-get-server-version-requests}

Adobe Access client 3.0 and higher send a Get Server Version request in order to determine the capabilities of the server. All servers using Adobe Access SDK 3.0 and higher must implement support for Get Server Version requests.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage` 
* The request URL must be “License Server URL in metadata” + “/flashaccess/getServerVersion/v3”

For Adobe Access SDK 4.0 and higher, the response to a Get Server Version request indicates to clients that the server supports versions 3 and 4 of the Adobe Access protocol.
