---
title: Handling License Return requests
description: Handling License Return requests
copied-description: yes
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
---
# Handling License Return requests{#handling-license-return-requests}

If the client application needs to return a license, it invokes the DRMManager.returnVoucher() Actionscript API to initiate the process. This API can work in an immediateCommit mode, or a confirmFirst mode. If immediateCommit is set to true, the client will delete the local license(s) immediately, without waiting for confirmation from the license server that it has received the request to return the license(s). The Adobe Access license server should process the request and send a response to the client. Whether or not the license server actually does anything with the request (such as decrement a license count for the given user) is up to the license server to decide.

* The request handler class is com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler 
* The request message class is com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

The minimum Adobe Access SDK version required is version 5; the request URL will be " `/flashaccess/lreturn/v5`". As with Domain De-Registration, the server should use `getRequestPhase()` to determine if the client is previewing a license return.
