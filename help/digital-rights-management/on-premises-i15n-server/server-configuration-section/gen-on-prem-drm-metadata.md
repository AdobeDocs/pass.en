---
title: Generate the On Premises DRM Metadata
description: Generate the On Premises DRM Metadata
copied-description: yes
exl-id: b42e3491-081b-45bf-bd00-8fb769a97446
---
# Generate the On Premises DRM Metadata{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] utility is included in the [!DNL create_metadata] folder. The point of this utility is to create an On Premises DRM Metadata that will initiate the client into performing the individualization process against the specified On Premises Individualization Server. 

1. Update the Primetime DRM Reference Implementation - Command Line Tools with the following files:

    * [!DNL CreateMetadata.jar] 
    * [!DNL commons-cli-1.2.jar] 
    * [!DNL createMetadata.properties]

       The two JAR files can reside in the [!DNL Command Line Tools/libs] folder. The [!DNL createMetadata.properties] file can reside next to the [!DNL flashaccesstools.properties] file.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Included is an [!DNL examplecreate.sh] script that demonstrates a sample creation of metadata. Be sure to configure the License Server URL and Individualization Server URL in both the script and properties files before attempting to generate metadata.

The inputs for the utility are as follows:

* `createMetadata.properties` - Properties file containing a default Policy, Certificate locations and passwords, etc. 
* `indivCert` - PKCS12 file containing Individualization Transport certificate 
* `indivURL` - URL of the On Premises Individualization Server

The output file is an On Premises DRM Metadata file that will be consumed by the DRM client. For example: 

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
