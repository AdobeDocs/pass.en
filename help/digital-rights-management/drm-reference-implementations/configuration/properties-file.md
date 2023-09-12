---
title: License server properties file
description: License server properties file
copied-description: yes
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
---
# License server properties file{#license-server-properties-file}

The license server references properties set in the [!DNL flashaccess-refimpl.properties] file. You can refer to that file directly for details about specific values, and for usage information about each property. A fully functional sample is provided in the [!DNL resources] directory of the reference implementation ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credentials** - The properties file includes settings for the location of the credentials that Adobe issues to you. You can specify these credentials in a [!DNL .pfx] file with a password, or provide an alias and password for a credential that is stored on an HSM. You need to at least configure the properties that are related to the Transport Credential and the License Server Credential. Specify the locations of your credential files relative to the directory that you specifiy in the `config.resourcesDirectory` property.

**Flash Media Rights Management Server** - The `flashaccess-refimpl.properties` file also includes several properties that are related to packaging content. These properties are used only for the Flash Media Rights Management Server 1.x metadata conversion. After modifying the values in this property file, for the changes take effect, restart the license server.
