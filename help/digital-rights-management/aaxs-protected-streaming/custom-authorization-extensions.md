---
title: Custom authorization extensions
description: Custom authorization logic may be invoked during license acquisition to decide if a license should be issued to the requesting client.
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
---
# Custom authorization extensions {#custom-authorization-extensions}

Custom authorization logic may be invoked during license acquisition to decide if a license should be issued to the requesting client.

To implement your own customer authorization extension, first look at the [!DNL SampleAuthorizer.java] sample code located in the samples directory (the compiled version of this sample is located in flashaccess-license-server-ext-sample.jar).

To build your own extension, implement the `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interface and make sure `flashaccess-license-server-exts.jar` and `commons-logging.jar` are on the build path `adobe-flashaccess-sdk.jar` must also be on the build path if you utilize certain fields in `IMessageFacade`). To deploy your extension, copy your jar or class files to *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. If you need to update the jar or class files, the server must be restarted before the updated version is used. You also must add the authorizer class name to the tenant configuration file.
