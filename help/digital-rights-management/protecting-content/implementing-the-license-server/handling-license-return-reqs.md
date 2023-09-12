---
title: Handle License Return requests
description: Handle License Return requests
copied-description: yes
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
---
# Handle License Return requests{#handle-license-return-requests}

If the client application needs to return a license, it invokes the `DRMManager.returnVoucher()` Actionscript API to initiate the process. This API can work in an `immediateCommit` mode or a `confirmFirst` mode. If `immediateCommit` is set to `true`, the client then deletes the local license(s) immediately without waiting for confirmation from the license server that it has received the request to return the license(s). The Adobe Primetime DRM license server should process the request and send a response to the client. Whether or not the license server processes the request, such as decrement a license count for a specified user, is decided by the license server.

*  The request handler class is `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler` 
*  The request message class is `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

The minimum `Adobe Primetime DRM` SDK version required is version 5; the request URL is " [!DNL /flashaccess/lreturn/v5]". As with Domain De-Registration, the server uses `getRequestPhase()` to determine if the client can preview a license return.
