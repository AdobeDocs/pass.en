---
title: Tenant configuration file
description: Tenant configuration file
copied-description: yes
exl-id: 0f6cafbe-99d9-43bc-9a7f-d87c4da1f37f
---
# Tenant configuration file {#tenant-configuration-file}

The flashaccess-tenant.xml configuration file contains settings that apply to a specific tenant of the license server. Each tenant has its own instance of this configuration file located in *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. See the [!DNL configs/flashaccessserver/tenants/sampletenant] directory for an example tenant configuration file.

You can specify all file paths in the tenant configuration file as absolute paths or paths relative to the tenant's configuration directory (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*).

The tenant configuration file includes:

* **Transport Credential** — Specifies one or more transport credentials (certificate and private key) issued by Adobe. Can be specified as a path to a .pfx file and a password, or an alias for a credential stored on an HSM. Several such credentials can be specified here, either as file paths, or key aliases, or both. See "[Handling certificate updates](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)" in *Using the Adobe Access SDK for Protecting Content* for more information on when additional credentials are needed. 
* **License Server Credential** — Specifies one or more license server credentials (certificate and private key) issued by Adobe. Can be specified as a path to a .pfx file and a password, or an alias for a credential stored on an HSM. Several such credentials can be specified here, either as file paths, or key aliases, or both. See Handling certificate updates in *Using the Adobe Access SDK for Protecting Content *for more information on when additional credentials are needed. 
* **Key Server Certificates** — Optional. Specifies the Key Server's License Server certificate issued by Adobe. Can be specified as a path to a .cer file or an alias to a certificate stored on an HSM. This option must be specified in order to issue licenses for content packaged with a policy that requires remote key delivery for iOS devices. 
* **Custom Authorizers** — Optional. Specifies custom authorizer classes to invoke for each license request. If multiple authorizers are specified, they are invoked in the order listed. For more information, see "[Custom authorization extensions](../../aaxs-protected-streaming/custom-authorization-extensions.md)". 
* **List of Authorized Packagers** — Optional. Specifies certificates identifying entities authorized to package content for this license server. If no packager certificates are specified, the server issues licenses for content packaged by any packager. 
* **Minimum supported client version** (See *Using the Adobe Access SDK for Protecting Content*). 
* **Usage Rules**

    * **License Caching** — Optional. Specifies how long the license can be stored on the client. By default license caching is disabled. To enable license caching for a limited time period, set the end date or the number of seconds for which the license should be stored (starting when the license is issued). Setting the number of seconds to 0 disables license caching.

      Note that all licenses issued by the Server for Protected Streaming have an expiration period of 24 hours (86400 seconds). This value therefore applies implicitly as an upper bound to whatever end date or duration is set for license caching as well, with a maximum value of 86400 seconds, even though the schema enforces higher bounds. 
    
    * **Play Right** — At least one right must be specified. If multiple rights are specified, the client will use the first right for which it meets all the requirements.

        * **Output Protection** — Controls whether output to external rendering devices should be protected. 
        * **AIR and SWF Application Restrictions** — Optional allow list of SWF and AIR applications that may play the content (i.e., only the applications specified are permitted). SWF applications are identified by a URL or by the digest of the SWF and the maximum time to allow for download and verification of the digest. For information on calculating the SWF digest, see the “SWF Hash Calculator” section. AIR and iOS applications are identified by a publisher ID and optional application ID, minimum version, and maximum version. If no application restrictions are specified, any SWF or AIR application may play the content. 
        * **DRM and Runtime Module Restrictions** — Specifies the minimum security level required for the DRM/Runtime module. Optionally includes a block list of versions that are not permitted to play the content. Module versions are identified by attributes such as operating system and/or a version number. DRM Module Restrictions and Runtime Module Restrictions now support the following additional attributes:

            * `oemVendor` 
            * `model` 
            * `screenType`

          The following attributes are now optional:

            * `osVersion` 
            * `version`

        * **Device capability requirements** — Optionally specifies the hardware capabilities required to access content. 
        * **Jailbreak detection requirements** — Optionally specifies that playback is not allowed for devices on which jailbreak is detected.

See the comments in the example tenant configuration file for more details.
