---
description: The flashaccess-tenant.xml configuration file includes settings that apply to a specific tenant of the license server.
title: Tenant configuration file
exl-id: 35ec521f-ba17-4a2d-8adb-82b2c6cbe33a
---
# Tenant configuration file{#tenant-configuration-file}

The flashaccess-tenant.xml configuration file includes settings that apply to a specific tenant of the license server.

Each tenant supports its own instance of this configuration file that is located in `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. See the `configs/flashaccessserver/tenants/sampletenant` directory for an example tenant configuration file.

You can specify all file paths in the tenant configuration file as absolute paths or as paths that are relative to the tenant's configuration directory (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

The tenant configuration file includes:

* *Transport Credential* — Specifies one or more transport credentials (certificate and private key) issued by Adobe. Can be specified as a path to a [!DNL .pfx] file and a password, or an alias for a credential stored on an HSM. Several such credentials can be specified here, either as file paths, or key aliases, or both.

  See *Handling certificate updates* in *Using the Adobe Primetime DRM SDK for Protecting Content* for more information on when additional credentials are needed. 

* *License Server Credential* — Specifies one or more license server credentials (certificate and private key) that Adobe has issued. You can specify the license server credentials as a path to a [!DNL .pfx] file and a password, or an alias for a credential stored on an HSM. Several such credentials can be specified here, either as file paths, or key aliases, or both.

  See *Handling certificate updates* in *Using the Adobe Primetime DRM SDK for Protecting Content* for more information on when additional credentials are needed. 

* *Key Server Certificates* — Optionally specifies the Key Server's License Server certificate that Adobe has issued. You can specify the Key Server's License Server certificate as a path to a [!DNL .cer] file or an alias to a certificate that is stored on an HSM. This option must be specified to issue licenses for content that is packaged with a DRM policy that requires remote key delivery for iOS devices. 

* *Custom Authorizers* — Optionally specifies custom authorizer classes to invoke for each license request. If multiple authorizers are specified, they are invoked in the order listed. 
* *List of Authorized Packagers* — Optionally specifies certificates that identify entities authorized to package content for this license server. If no packager certificates are specified, the server issues licenses for content that is packaged by any packager. If the server receives a license request from an unauthorized packager, then the request is denied. 
* *Minimum supported client version* See Using the Adobe Primetime DRM SDK for Protecting Content. 

* *Usage Rules*

    * *License Caching* — Optionally specifies how long you can store the license on the client. By default license caching is disabled. If you want to enable license caching for a limited time period, you need to set the end date or the number of seconds for which the license should be stored (starting when the license is issued). Setting the number of seconds to 0 disables license caching.     
    
      >[!NOTE]
      >
      >All licenses that the Server for Protected Streaming has issued include an expiration period of 24 hours (86400 seconds). This value applies implicitly as an upper bound to whatever end date or duration is set for license caching as well, with a maximum value of 86400 seconds, even though the schema enforces higher bounds.

    * *Play Right* — A minimum of one right must be specified. If you specify multiple rights, then the client uses the first right that meets all the requirements.

        * *Output Protection* — Controls whether output to external rendering devices should be protected. 
        * *AIR and SWF Application Restrictions* — Optional allow list of SWF and AIR applications that may play the content (for example, only the applications specified are permitted). SWF applications are identified by a URL or by the digest of the SWF and the maximum time to allow for download and verification of the digest.

          See *SWF Hash Calculator* for information on how to calculate the SWF digest.

          A publisher ID and optional application ID, minimum version, and maximum version identify AIR and iOS applications. If you do not specify any application restrictions, then any SWF or AIR application can play the content. 
        
        * *DRM and Runtime Module Restrictions* — Specifies the minimum security level required for the DRM/Runtime module. Optionally includes a block list of versions that are not permitted to play the content. Module versions are identified by attributes, such as operating system and/or a version number.

          DRM Module Restrictions and Runtime Module Restrictions now support the following additional attributes:

            * `oemVendor` 
            * `model` 
            * `screenType`

          The following attributes are now optional:

            * `osVersion` 
            * `version`

        * *Device capability requirements* — Optionally specifies the hardware capabilities required to access content. 
        * *Jailbreak detection requirements* — Optionally specifies that playback is not allowed for devices on which jailbreak is detected.

See the comments in the example tenant configuration file for more details.
