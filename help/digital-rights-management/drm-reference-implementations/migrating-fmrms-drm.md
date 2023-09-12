---
description: To continue issuing licenses for content that has been packaged with Flash Media Rights Management Server (FMRMS) 1.0 or 1.5, you must migrate license and DRM policy data from the LiveCycle ES server to the customer's new server that is based on the Adobe Primetime DRM SDK.
title: Migrate from FMRMS 1.0 or 1.5 to Adobe Primetime DRM 2.0 or later
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
---
# Migrate from FMRMS 1.0 or 1.5 to Adobe Primetime DRM 2.0 or later{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

To continue issuing licenses for content that has been packaged with Flash Media Rights Management Server (FMRMS) 1.0 or 1.5, you must migrate license and DRM policy data from the LiveCycle ES server to the customer's new server that is based on the Adobe Primetime DRM SDK.

To migrate, complete the following tasks:

1. Import license information:

    1. To import license information from LiveCycle ES to your Primetime DRM -based server, see the sample database scripts in the [!DNL Reference Implementation\Server\migration\db] folder. 
    1. Run the sample scripts to export relevant data from a MySQL, Oracle, or SQL Server database to a CSV file format. 
    1. After you export the data from LiveCycle ES, import the data to your database.

       The exported license information includes the following:

        * A license ID 
        * A Content ID that is assigned at packaging time 
        * The ID of the DRM policy that is being applied 
        * The time the content was packaged 
        * The content encryption key

       This information is required before you can convert the 1.x content metadata to the Primetime DRM metadata format. In the reference implementation, this data is stored in the License database table and is used by `RefImplMetadataConvReqHandler`. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.

1. Convert FMRMS policies to the Primetime DRM format:

    1. Before you can apply the DRM policies to convert metadata and issue licenses for version 1.0 or version 1.5 content, convert existing DRM policies to the Primetime DRM format.

       The `Reference Implementation\Server\migration` folder includes sample code to create a Primetime DRM policy that is based on older DRM policies. To migrate from FMRMS 1.0 to Primetime DRM , see the `V1_0PolicyConverter.java` sample. 
    1. Compile the sample code by running `ant-f build-migration.xml build-1.0-converter` script, which searches for the 1.0 and Primetime DRM libraries in the [!DNL libs/1.0] and [!DNL libs/flashaccess] directories. 
    
    1. Edit the [!DNL converter.properties] file to point to your LiveCycle ES server. 
    1. Run `ant -f build-migration.xml migrate-all-1.0-policies` to convert all FMRMS 1.0 DRM policies to Primetime DRM format.

       To migrate from FMRMS 1.5 to Primetime DRM , see the `V1_5PolicyConverter.java` sample. 
    
    1. Compile the sample code by running `ant-f build-migration.xml build-1.5-converter` script, which expects the 1.5 and 3.0 libraries to be in the [!DNL libs/1.5] and [!DNL libs/flashaccess] directories. 
    
    1. Edit the [!DNL converter.properties] file to point to your LiveCycle ES server. 
    1. Run `ant -f build-migration.xml migrate-all-1.5-policies` to convert all FMRMS 1.5 DRM policies to Primetime DRM format.

       The converted DRM policies are saved as a set of files. The `DRM PolicyConverter` generates a CSV-formatted file that includes the mapping of the old DRM policy IDs to the new DRM policy IDs. You can import this file to the [!DNL PolicyConversion] table in the reference implementation database, where it is used by `RefImplMetadataConvReqHandler`.

1. Support the 1.x compatibility requests with the `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler` properties:

    1. After the relevant data has been migrated to an Primetime DRM-based server, implement support for 1.x compatibility requests.

       For examples about how to process these types of requests, see `RefImplUpgradeV1ClientHandler` and `RefImplMetadataConvReqHandler` in the reference implementation.
