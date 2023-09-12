---
title: Migrating from FMRMS 1.0 or 1.5 to Adobe Access 2.0 and above
description: Migrating from FMRMS 1.0 or 1.5 to Adobe Access 2.0 and above
copied-description: yes
exl-id: 9aadf9a0-a7c5-466b-9dd1-c1bab2b8bfc6
---
# Migrating from FMRMS 1.0 or 1.5 to Adobe Access 2.0 and above {#migrating-from-fmrms-or-to-adobe-access-and-above}

In order to continue to issue licenses for content packaged using Flash Media Rights Management Server (FMRMS) 1.0 or 1.5, license and policy data must be migrated from the LiveCycle ES server to the customer's new server based on the Adobe Access SDK. The important steps are:

1. Importing license information 
1. Converting FMRMS policies to Adobe Access format 
1. Supporting the 1.x compatibility requests via the `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`

To import license information from LiveCycle ES into your Adobe Access-based server, refer to the sample database scripts provided in the [!DNL Reference Implementation\Server\migration\db] folder. Sample scripts are provided for exporting the relevant data from a MySQL, Oracle, or SQL Server database into a CSV file format. Once the data is exported, it can be imported into the database of your choice. The exported license information includes the License ID, a Content ID assigned at packaging time, the ID of the Policy used, the time the content was packaged, and the content encryption key. For Adobe Access, this information is required in order to convert the 1.x content metadata into the Adobe Access metadata format (see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`). In the reference implementation, this data is stored in the License database table and used by `RefImplMetadataConvReqHandler`.

Existing policies will need to be converted to the Adobe Access format in order to use those policies when converting metadata and issuing licenses for 1.0 or 1.5 content. The Reference Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

If you are migrating from FMRMS 1.0 to Adobe Access, see the V1_0PolicyConverter.java sample. Compile the sample code by running " `ant-f build-migration.xml build-1.0-converter`" (the script expects the 1.0 and Adobe Access libraries to be in [!DNL libs/1.0] and libs/flashaccess respectively). Edit the converter.properties file to point to your LiveCycle ES server. Then run " `ant -f build-migration.xml migrate-all-1.0-policies`" to convert all FMRMS 1.0 policies to Adobe Access format.

If you are migrating from FMRMS 1.5 to Adobe Access, see the V1_5PolicyConverter.java sample. Compile the sample code by running " `ant-f build-migration.xml build-1.5-converter`" (the script expects the 1.5 and 3.0 libraries to be in libs/1.5 and libs/flashaccess respectively). Edit the converter.properties file to point to your LiveCycle ES server. Then run " `ant -f build-migration.xml migrate-all-1.5-policies`" to convert all FMRMS 1.5 policies to Adobe Access format.

The converted policies will be written to a set of files. In addition, PolicyConverter will output a CSV file containing the mapping of old policy IDs to new policy IDs. This file can be imported into the "PolicyConversion" table in the reference implementation database, and will be used by `RefImplMetadataConvReqHandler`.

Once the relevant data has been migrated to your Adobe Access-based server, you are ready to implement support for 1.x compatibility requests. See `RefImplUpgradeV1ClientHandler` and `RefImplMetadataConvReqHandler` in the reference implementation for examples of how to process these types of requests.
