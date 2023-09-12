---
title: Securely packaging content
description: Securely packaging content
copied-description: yes
exl-id: f554852c-83d9-4b31-8dde-2af577c70989
---
# Securely packaging content {#securely-packaging-content}

The configuration file for the Adobe Access Media Packager command line tool requires a PKCS12 credential that is used during packaging.

In the Reference Implementation Command Line tools, the password for the PKCS12 credentials file is stored in the flashaccess.properties file in clear text. For this reason, take extra care when securing the computer hosting this file, and ensure that it is in a secure environment. (See [Physical security and access](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

The packager also uses the License Server and License Server Transport certificates. Both the integrity and confidentiality of this information must be protected. Only authorized entities should be permitted to use the packager. If any of your private keys are compromised, immediately inform Adobe Systems Incorporated so that the certificate can be revoked.

>[!NOTE]
>
>The API allows you to use the same key for multiple pieces of content. To ensure the highest level of security, we recommend this feature only be used for multi-bit rate FMS content. It is not recommended to use the same key for multiple files representing different content.

The Adobe Access Packaging API issues warnings under certain conditions. You must review these warnings to determine whether your files have been successfully encrypted. The warning messages may state that the policy has expired, an unrecognized tag or track will not be encrypted, movie fragments will not be encrypted (and references inside those fragments may become invalid), and metadata will not be encrypted.

If content is packaged using a policy with incorrect attributes, the policy should be updated, and the updated policy must be made available to the License Server though a policy update list or another mechanism for delivering the updated policy to the server. Some policy attributes cannot be changed after the policy is created. If these attributes are incorrect, pull the content back from the distribution sites, revoke the policy so that no future licenses can be granted, and re-encrypt the content.

When packaging is complete, the packaging key is not explicitly destroyed; however, it is garbage-collected. Therefore, the packaging key does remain present in memory for a period of time; you must guard against unauthorized access to the machine and take steps to ensure that you do not expose any files, such as core dumps, that may reveal this information.
